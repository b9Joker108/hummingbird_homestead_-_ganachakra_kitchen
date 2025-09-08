# Smarthome Notes #

Goals and threat model

You’re putting a voice-controllable agent in a space with heat, blades and distractions. Governance has to be explicit, layered and fail-safe.

- Primary goals: Hands-free control, fast responses, no accidental activations, bounded authority, complete auditability.
- Threats to mitigate: Accidental triggers (music/TV/podcasts), guests/children issuing commands, replay attacks from digitization, GenAI generations and recordings, device theft, command injection over Internet and/or network, over-privileged automations.

---

Identity and authentication for voice

Treat “who is speaking” and “what they can do” as separate layers. Voice is a convenient signal, not the sole source of truth.

- Enrollment: 
  - Capture 5–10 varied utterances (quiet, cooking noise) for each authorized user.
  - Store voiceprints locally, encrypted at rest; never sync raw audio.
- Wake word + push-to-talk:
  - Wake word: Custom per household member reduces ambient triggers.
  - Hold-to-talk: A capacitive or BLE button in the kitchen cuts false positives even more.
- Speaker verification:
  - Use text-independent verification on every command after the wake word.
  - Require a short per-user passphrase for sensitive scopes (e.g., “Confirm with cinnamon”).
- Presence as a factor:
  - Combine voice with proximity (phone/BLE/NFC ring) for step-up auth.
  - No presence → allow only low-risk commands; grant elevation only with verbal MFA.

---

Command governance model

Use a capability-first model with role overlays, enforced by a policy engine.

- Capabilities (fine-grained):
  - Examples: control.timer.start, control.music.play, control.lights.dim, info.read.shopping-list, device.oven.preheat.
- Roles (coarse):
  - guest, resident, admin; map each to a set of capabilities with constraints.
- Policy engine:
  - Evaluate: user, capability, context (time, presence, device state, noise level).
  - Deny by default; require explicit allow with constraints.

Example policy (YAML):
```yaml
users:
  beauford:
    roles: [admin]
    presence: ble:phone_beauford
roles:
  guest:
    allow:
      - control.music.play
      - control.timer.start
  resident:
    allow:
      - control.lights.*
      - info.read.*
      - control.music.*
      - control.timer.*
  admin:
    allow:
      - "*"
    deny:
      - device.oven.* if presence != "ble:phone_beauford"
      - device.lock.open if time not_in "08:00-21:00"
capabilities:
  device.oven.preheat:
    requires: [speaker_verified]
    stepup: [verbalpinorble]
  device.lock.open:
    requires: [speaker_verified, passphrase]
```

---

Temporary privilege elevation by voice (safe and revocable)

Grant short-lived, attenuated tokens instead of flipping global switches.

- Elevation phrase (explicit):
  - “Elevate for oven control 10 minutes.”
- Issue capability tokens:
  - Mint a signed, time-boxed token with caveats (who, what, where, when).
  - Store in memory only; auto-expire and revoke on “cancel elevation.”
- Attenuation (least privilege):
  - Scope down to specific device and bounds (e.g., max 200°C, single preheat).
- Step-up authentication:
  - Require a verbal PIN/passphrase or detect BLE presence for high-risk scopes.
  - If noise level is high or verification confidence is low, refuse and ask to repeat close to mic or use the button.

Example token (JWT-like claims or macaroons):
```json
{
  "sub": "beauford",
  "cap": ["device.oven.preheat"],
  "constraints": {
    "device_id": "oven-01",
    "maxtempc": 200,
    "uses": 1,
    "room": "kitchen"
  },
  "aud": "home-orchestrator",
  "nbf": 1694100000,
  "exp": 1694100600,
  "auth": ["speakerverified", "blepresence"]
}
```

Revocation and audit:
- Voice command: “Cancel oven elevation.”
- Automatic: On door open, house empty, or smoke alarm → revoke all tokens.
- Audit log: Append-only, local, with per-event hash chain.

---

On-device architecture components (Termux/Debian, Python, JS/TS)

- Audio I/O:
  - Always-on wake-word listener with VAD; push-to-talk GPIO/BLE optional.
- ASR + NLU:
  - On-device ASR model; intent parser with a strict command grammar and slot filling.
- Speaker verification:
  - Text-independent embedding + cosine threshold; cache recent embeddings for speed.
- Policy and tokens:
  - Python policy service (FastAPI) evaluates YAML/rego policies; issues short-lived macaroons/JWTs with caveats.
- Orchestrator:
  - Routes authorized intents to backends (Home Assistant/Matter/MQTT/custom scripts).
- Presence/MFA bridges:
  - BLE scanner for trusted devices; optional NFC tap for instant step-up.
- Audit and safety:
  - Structured logs (JSON) with per-entry SHA chaining; watchdog that can hard-disable risky domains on alerts.

Suggested process boundaries:
- Mic/ASR sandboxed, minimal privileges.
- Policy engine isolated, holds signing keys.
- Actuator adapters accept only signed capability tokens.

---

Practical flows

Low-risk command (no elevation)
1. “Hey Beauford, set a 7-minute timer.”
2. Wake, ASR, NLU → intent control.timer.start.
3. Speaker verified (OK). Policy: resident allows. Execute. “Timer set.”

Sensitive command with elevation
1. “Hey Beauford, preheat oven to 190°C.”
2. Policy: requires elevation. “I can do that with your authorization. Say your passphrase or tap your phone.”
3. Passphrase verified + BLE present → issue token (oven preheat ≤200°C, 10 minutes).
4. Execute with token; confirm: “Preheating to 190°C for the next 10 minutes.”

Revocation
- “Cancel oven authorization.” → Revoke token family; “Authorization revoked.”

---

Hard safety limits and auditing

- Immutable guardrails: Certain actions permanently capped (max temp, no unlocks after 21:00) regardless of role.
- Two-channel confirmation: For irreversible actions, require both passphrase and proximity.
- Noise-aware refusals: If SNR is poor, refuse sensitive operations.
- Offline-first: No cloud dependency for auth/ASR; cloud optional for non-critical features.
- Transparent logs: “At 18:42, Beauford authorized oven preheat for 10 minutes (BLE present).”

---

If you want, I can draft:
- A minimal FastAPI policy service that mints time-boxed capability tokens.
- A YAML policy skeleton tuned to your kitchen devices and routines.
- A ZSH harness to enroll voiceprints and manage passphrases securely on Termux.

  

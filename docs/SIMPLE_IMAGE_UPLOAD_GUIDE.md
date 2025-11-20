# SIMPLE: How to Share Images - 3 Steps

## The Native Method: Screenshot + Paste

This is **THE** quick and easy native way to share images on GitHub:

---

### Step 1: Take Screenshot
Press your device's screenshot shortcut:
- **Windows**: `Win + Shift + S`
- **Mac**: `Cmd + Shift + 4`
- **Linux**: `PrtScn` or `Shift + PrtScn`
- **Android**: `Power + Volume Down`
- **iOS**: `Side Button + Volume Up`

---

### Step 2: Go to PR Comment Box
- Open this PR on **github.com** in a web browser
- Scroll to the bottom
- Click in the large text box that says "Add a comment"

---

### Step 3: Paste
- Press `Ctrl + V` (Windows/Linux) or `Cmd + V` (Mac)
- Wait 1-2 seconds
- You'll see `![image](https://...)` appear
- Click "Comment" button

---

## That's It!

The image is now shared. No drag-and-drop needed, no files to save, no buttons to find.

**Screenshot → Go to PR → Paste → Done**

---

## Still Having Issues?

### If paste doesn't work:
1. **Make sure you're on github.com** (not a mobile app or third-party site)
2. **Click inside the text box first** before pressing Ctrl+V
3. **Try a different browser** (Chrome or Firefox recommended)
4. **Disable browser extensions** temporarily (ad blockers can interfere)

### Alternative: Add to repository
If you really can't upload via comment:

```bash
# Save your screenshot to the repository
cp ~/screenshot.png assets/images/my_commit_screenshot.png

# In the PR comment, just mention:
"I've added the screenshot to assets/images/my_commit_screenshot.png"
```

Then I can view it in the repository.

---

## Common Confusion

**"Where is the chat?"** → You're already in it! The PR comment section IS the interface for communicating with Copilot. There's no separate chat window. All communication happens via PR comments on github.com.

**"Drag-and-drop doesn't work"** → That's okay! Paste (Ctrl+V) is actually better and more reliable. Use that instead.

**"I see content:// URL"** → That's a local device path. Use the paste method above instead of trying to share that URL.

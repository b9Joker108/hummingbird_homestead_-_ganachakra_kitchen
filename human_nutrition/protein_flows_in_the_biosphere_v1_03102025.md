File: https://github.com/b9Joker108/hummingbird_homestead_-_ganachakra_kitchen/blob/main/human_nutrition/protein_flows_in_the_biosphere_v1_03102025.md

This really should be better placed in the repo. I need a dedicated and structured subdirectory for functions, cli one-liners and shell scripts, etc. **TODO**
...


Here’s a rigorously annotated, POSIX‑conforming shell script designed for Termux (or any GNU/Linux environment). It is modular, functional, and prompts the user both for the input .docx file and the desired output .md path. The script uses pandoc under the hood for conversion, but is structured so you can swap in another converter if desired.

---

```bash

!/bin/sh



docx2gfm.sh — Elegant DOCX → GitHub‑flavored Markdown converter

POSIX‑conforming, modular, and annotated for clarity.



Requirements:

- pandoc installed in Termux (pkg install pandoc)

- libreoffice (optional, for legacy .doc conversion)



Usage:

./docx2gfm.sh



The script will:

1. Prompt user for input DOCX file

2. Prompt user for output Markdown file path

3. Convert DOCX → GFM Markdown with media extraction

4. Report success or failure



#########################################################################

Utility functions

#########################################################################

Print a message to stderr
say() {
    printf '%s\n' "$*" >&2
}

Exit with error message
die() {
    say "ERROR: $*"
    exit 1
}

Prompt user for input with a message
prompt() {
    # $1 = prompt message
    # result echoed to stdout
    printf '%s: ' "$1" >&2
    read ans || die "Input aborted"
    printf '%s' "$ans"
}

#########################################################################

Conversion function

#########################################################################

convertdocxto_md() {
    in_file=$1
    out_file=$2
    media_dir=$3

    # Ensure input exists
    [ -f "$infile" ] || die "Input file not found: $infile"

    # Run pandoc conversion
    pandoc "$in_file" \
        -t gfm \
        --extract-media="$media_dir" \
        -o "$out_file" \
        || die "Conversion failed"

    say "Converted: $infile → $outfile"
    say "Media extracted to: $media_dir"
}

#########################################################################

Main program flow

#########################################################################

main() {
    say "=== DOCX → GitHub‑flavored Markdown Converter ==="

    # Prompt for input file
    in_file=$(prompt "Enter path to input .docx file")
    [ -n "$in_file" ] || die "No input file specified"

    # Prompt for output file
    out_file=$(prompt "Enter path to save output .md file")
    [ -n "$out_file" ] || die "No output file specified"

    # Derive media directory alongside output
    basename=$(basename "$outfile" .md)
    mediadir="media${base_name}"

    # Perform conversion
    convertdocxtomd "$infile" "$outfile" "$mediadir"

    say "=== Conversion complete ==="
}

Execute main only if script is run directly

(allows sourcing for reuse of functions)
if [ "${0##*/}" = "docx2gfm.sh" ] || [ "$0" = "./docx2gfm.sh" ]; then
    main "$@"
fi
```

---

✨ Features
- POSIX‑conforming: uses only portable sh syntax, no Bash‑isms.  
- Modular: functions (say, die, prompt, convertdocxto_md, main) are reusable.  
- Interactive: prompts user for input and output paths elegantly.  
- Integrity: checks for file existence, aborts gracefully on error.  
- Media handling: extracts embedded images into a dedicated folder named after the output file.  

---

Example Run
`text
$ ./docx2gfm.sh
=== DOCX → GitHub‑flavored Markdown Converter ===
Enter path to input .docx file: report.docx
Enter path to save output .md file: report.md
Converted: report.docx → report.md
Media extracted to: media_report
=== Conversion complete ===
`

---

Would you like me to extend this into a batch‑mode variant (looping over multiple .docx files in a directory) while still preserving the interactive prompts for output location? That would give you both single‑file elegance and multi‑file grunt power.


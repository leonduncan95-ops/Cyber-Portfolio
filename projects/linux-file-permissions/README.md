# Linux File Permissions (Access Cleanup)

## One-line summary
Checked file/folder permissions in Linux and fixed access so only the right users/groups could read or change files.

## Tools used
- Linux CLI
- chmod
- ls

## What I did (high level)
1. Checked permissions using `ls -l` and `ls -la` (including hidden files).
2. Reviewed what the permission string means (who can read/write/execute).
3. Updated permissions with `chmod` to remove access that shouldn’t be there.
4. Re-checked results to confirm the changes worked.

## Why this matters
This is a basic but important security skill — if permissions are too open, the wrong person can edit or view sensitive files.

## Files
- File permissions in Linux (PDF/DOCX)


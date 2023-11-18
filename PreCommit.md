## !nocommit - Pre-commit hook for preventing accidental commits

To prevent debug code from being accidentally committed, simply add a comment near your debug code containing the keyword `!nocommit` and this script will abort the commit.

### Setup

Paste this script in your `.git/hooks/pre-commit` file (create one if it doesn't exist yet).

```bash
if git commit -v --dry-run | grep '!nocommit' >/dev/null 2>&1
then
  echo "Trying to commit non-committable code."
  echo "Remove the !nocommit string or unstaging and try again."
  exit 1
else
  exit 0
fi
```

### Global Configuration
1. Add a global hooks directory to git config `core.hookspath=/Users/<username>/hooks`
2. In the directory, create a file named pre-commit.
3. Make sure this has execution rights. `chmod +x /Users/<username>/hooks/pre-commit`

### Webstorm configuration for special highlighting
1. Abuse the editor's ability to add custom TODO keywords Editor -> TODO
2. Pattern `.*\!nocommit.*`
3. Colors FG: `#E21C21`, BG: `#39BFCA`, Error stripe: `#F954D7`, Effects: `#EDF8FF`, bordered. 

#### Additional thoughts
- Haven't tested this on Windows.
- Might need a shebang `#!/bin/sh` on some platforms.

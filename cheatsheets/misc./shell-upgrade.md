---
description: Upgrading shell for more functionality.
---

# Shell Upgrade

### Linux

```bash
script -qc /bin/bash /dev/null
# Ctrl + Z to bg current session
stty raw -echo ;fg
export TERM=xterm-256color
```


---
title: "Show current git branch"
description: "Stop making mountains out of molehills"
date: "2018-08-23"
---

During development, it can be quite convenient to always know which branch you are on without having to do a git status. Most developers install a bash script and modify the prompt string 1 (PS1)  variable of their shell. I was most developers. Now, I just visit this article and copy paste the following into my `~/.bash_profile`:

```bash
# Show current git branch when entering a git repository
export PS1="\W \[\e[0;36m\]\$(git rev-parse --abbrev-ref HEAD 2> /dev/null)\[\e[0m\]\$ "
```

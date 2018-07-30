---
title: "Show current git branch"
description: "Stop making mountains out of molehills"
date: "2018-08-23"
tags: ["tooling", "bash"]
---

During development, it can be quite convenient to always know which branch you are on without having to do a git status. Most developers use sophisticated bash scripts to modify the prompt string 1 (PS1)  variable of their shell. As embarrassing as it is, I was most developers (I even had my own repo with a "performance" focused approach). Now, I simply use a one-liner. In fact, I just visit this article and copy paste the following into my `~/.bash_profile`:

```bash
# Show current git branch when entering a git repository
export PS1="\W \[\e[0;36m\]\$(git rev-parse --abbrev-ref HEAD 2> /dev/null)\[\e[0m\]\$ "
```

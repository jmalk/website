---
title: Git HEAD is stored in a text file
tags: til
---

# Git HEAD is stored in a text file

The current value of `HEAD` is stored as human-readable text in a file in the `.git` directory. You can check it with `cat .git/HEAD` (or whatever your preferred way of reading text files is).

I learned this while checking my (previously somewhat shaky) mental model of what git HEAD even is. It refers to the bit of the commit tree you currently have checked out. Typically that'll be a branch name, but it could also be a commit not associated with a branch - the "detached HEAD state" you might see mentioned in output from git commands.

## Sources

- [Stack Overflow: What is HEAD in Git Answer](https://stackoverflow.com/a/2304106)
- [Pro Git, 10.3 Git Internals - Git References](https://git-scm.com/book/en/v2/Git-Internals-Git-References)
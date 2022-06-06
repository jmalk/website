---
title: Fixing Tests with Git Bisect
tags: learning
---
# Fixing Tests with Git Bisect

I love git bisect so I'm gonna share it in case anyone doesn't know it. "Which commit did I break this unit test in? It was fine this morning..." =>

```
git bisect start HEAD <good-commit-hash-from-this-morning>
git bisect run npm test
# Or in our case:
# git bisect run npm --prefix ./app/ test
git bisect reset
```

Does binary search for the first commit to fail npm test.

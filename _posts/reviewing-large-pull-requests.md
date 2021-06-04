---
layout: post
title: Reviewing large pull requests
subtitle: How I got my 13k lines PR merged
tags: [programming]
---

In my team we use GitHub's pull request feature (PR) to do our code reviews. I don't think this is something unknown to the average developer reading this post, so I'll skip introducing it and come straight to how we use it in my team.

Usually getting a review for a PR takes from a couple of minutes to a few days, depending on its size. If everything's fine, the reviewer approves the PR, and it'll get merged. If the reviewer has remarks, he writes some comments, and the PR author either adjusts the code or replies to the comment. In this way all the discussions happen close to the code. After everything is resolved, the PR gets approved and merged.

But when I was assigned a large task some months ago, the PR ended up like this:

![Pi Zero with accessiores](/assets/img/post-review-large-prs/gh-pr-changes.png)

Phew! Almost 13,000 changed lines of code. Although this PR contained some refactoring that's easier to review, it's still quite a large pull request. Some days went by and no colleague picked up the PR.
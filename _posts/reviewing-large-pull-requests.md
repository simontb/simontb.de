---
layout: post
title: Reviewing large pull requests
subtitle: How I got my 13k lines PR merged
tags: [programming]
---

In my team we use GitHub's pull request feature (PR) to do our code reviews. I don't think this is something unknown to the average developer reading this post, so I'll skip introducing it and come straight to how we use it in my team.

Usually getting a review for a PR takes from a couple of minutes to a few days, depending on its size. If everything's fine, the reviewer approves the PR, and it'll get merged. If the reviewer has remarks, he writes some comments, and the PR author either adjusts the code or replies to the comment. In this way all the discussions happen close to the code. After everything is resolved, the PR gets approved and merged.

But when I was assigned a large task some months ago, the PR ended up like this:

![Screenshot of pull request size](/assets/img/post-review-large-prs/gh-pr-changes.png)

Phew! Almost 13,000 changed lines of code. Although this PR contained some refactoring that's easier to review, it's still quite a large pull request. Some days went by and no colleague picked up the PR. As due date came closer, I asked two colleagues that are involved in the topic if they could review my PR. Because of its size they were a bit hesitant, so we agree on having a review meeting to discuss the code directly.

todo: zu grosse prs oft nicht ausreichend gereviewt

##Having a code review meeting
Getting my code reviewed in a meeting was something new to me. As I said earlier, I'm more used to code being reviewed in GitHub (or other tools). I set up the meeting and looked forward to it.

As we're still working mostly remotely, we had to meet virtually. Our approach was that one of my colleagues opened the PR and shared his screen. We then scrolled through the changes and discussed the code.

When my colleagues spotted some things to improve, they told me and wrote a short PR comment. Some follow-up tasks arose that I just noted for myself. Sometimes they had questions and we could directly discuss them which speeded up the PR review process enormously. At the end of the meeting one collegue ran my code and gave further feedback.

The meeting took one hour and was very productive. Afterwards all changes were reviewed and I knew what I had to do before my PR could finally be merged.

Overall my PR was almost fine, so it took only a day to implement the requested changes. We didn't set up a follow-up meeting, but I simply pushed the changes and my colleagues only had a look at them instead of the full PR again. After all, the PR had been merged the day after our meeting.

##Our conclusion
We later discussed our approach in our regular retrospective meeting. We all agreed that I was a good idea to review such a large PR in a meeting instead of following the usual process.

Hopefully it won't happen anytime soon, but if we'll have such a PR again, I'd definitely propose a code review meeting then. 
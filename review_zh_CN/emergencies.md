# Emergencies 紧急情况

有时候有些代码变更要尽可能快的通过整个审查过程

## What Is An Emergency? 怎么样算作紧急情况？ {#what}

紧急代码变更应该是尽可能小的：确保发布继续而不是回滚的变更，修复严重影响产品终端用户的变更，处理紧迫法律问题的变更，关闭严重漏洞的变更等等。

紧急变更中，我们关心整个审查过程的速度，而不是审查响应的速度 [speed of response](reviewer/speed.md)。
只有在这种情况下，相比其他问题，审查者需要更多的关心审查速度和代码的正确性(代码是否真的能处理紧急问题)。
显然的，紧急代码变更的审查优先级高于其他代码审查过程。

无论怎样，紧急情况处理完毕后，你应该重新审查这些变更并给出深入的审查意见 [more thorough review](reviewer/looking-for.md).

## What Is Not An Emergency? 怎样不算是紧急情况 {#not}

To be clear, the following cases are *not* an emergency:

-   Wanting to launch this week rather than next week (unless there is some
    actual [hard deadline](#deadlines) for launch such as a partner agreement).
-   The developer has worked on a feature for a very long time and they really
    want to get the CL in.
-   The reviewers are all in another timezone where it is currently nighttime or
    they are away on an off-site.
-   It is the end of the day on a Friday and it would just be great to get this
    CL in before the developer leaves for the weekend.
-   A manager says that this review has to be complete and the CL checked in
    today because of a [soft (not hard) deadline](#deadlines).
-   Rolling back a CL that is causing test failures or build breakages.

And so on.

## What Is a Hard Deadline? 怎样是不容变更的 Deadline ？{#deadlines}

如果你错过了它会发生灾难性的事件，那这就是一个不容变更的 deadline。比如：

-   合同中明确规定截止日期的情况。
-   如果截止日期不发布将导致产品失败的情况。
-   Some hardware manufacturers only ship new hardware once a year. If you miss
    the deadline to submit code to them, that could be disastrous, depending on
    what type of code you’re trying to ship.

Delaying a release for a week is not disastrous. Missing an important conference
might be disastrous, but often is not.

Most deadlines are soft deadlines, not hard deadlines. They represent a desire
for a feature to be done by a certain time. They are important, but you
shouldn’t be sacrificing code health to make them.

If you have a long release cycle (several weeks) it can be tempting to sacrifice
code review quality to get a feature in before the next cycle. However, this
pattern, if repeated, is a common way for projects to build up overwhelming
technical debt. If developers are routinely submitting CLs near the end of the
cycle that "must get in" with only superficial review, then the team should
modify its process so that large feature changes happen early in the cycle and
have enough time for good review.

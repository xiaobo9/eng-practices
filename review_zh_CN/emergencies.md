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

大多数截止日期不是硬截止时间。它们表示希望在一定时间之前完成某项功能。
它们很重要，但是不应该为了完成该功能而牺牲代码质量。

如果发布周期较长（几周），可能会牺牲代码审查质量，在下一个周期之前把功能合并进来。
但是，这种模式，如果多次出现的话，是项目积累压倒性技术债务的一种常见方式。
如果开发人员常规地在周期结束时提交 "必须要合并" 的代码变更 CL，而这些 CL 仅进行了表面审核。
则团队必须修改流程，以便在周期的早期进行大的功能更改，并有足够的时间进行良好的审核。

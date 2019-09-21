# Writing good CL descriptions 编写良好的代码变更说明（提交记录）

代码变更描述需要说明 `在做什么` 和 `为什么这么做` 这两个问题。
它将被记录在我们的版本控制历史中，并且除了代码审查者之外，以后的数年中将有很多人会阅读它。

将来的开发人员会更新描述信息来搜索你的代码变更记录。将来有些人可能根据一些模糊的记忆来检索你的代码变更。
如果所有的重要信息都在代码中，而不是代码描述中，那么定位相关的代码变更将会非常的困难。（译者注：说的真对啊。。。）

## First Line 第一行 {#firstline}

* Short summary of what is being done. 简单描述将要做什么
* Complete sentence, written as though it was an order. 像命令一样的完整语句。
* Follow by empty line. 后面紧跟着一个空行。

代码提交记录的 `第一行` 应该概述做了什么样的修改，然后是一个空行。
第一行应该有足够的信息，以便将来的大部分开发人员了解你的代码变更做了什么，而不需要详细阅读代码内容或者完整的提交记录信息。

By tradition, the first line of a CL description is a complete sentence, written
as though it were an order (an imperative sentence). For example, say
\"**Delete** the FizzBuzz RPC and **replace** it with the new system." instead
of \"**Deleting** the FizzBuzz RPC and **replacing** it with the new system."
You don't have to write the rest of the description as an imperative sentence,
though.

## Body is Informative {#informative}

The rest of the description should be informative. It might include a brief
description of the problem that's being solved, and why this is the best
approach. If there are any shortcomings to the approach, they should be
mentioned. If relevant, include background information such as bug numbers,
benchmark results, and links to design documents.

Even small CLs deserve a little attention to detail. Put the CL in context.

## Bad CL Descriptions {#bad}

"Fix bug" is an inadequate CL description. What bug? What did you do to fix it?
Other similarly bad descriptions include:

-   "Fix build."
-   "Add patch."
-   "Moving code from A to B."
-   "Phase 1."
-   "Add convenience functions."
-   "kill weird URLs."

Some of those are real CL descriptions. Their authors may believe they are
providing useful information, but they are not serving the purpose of a CL
description.

## Good CL Descriptions {#good}

Here are some examples of good descriptions.

### Functionality change

> rpc: remove size limit on RPC server message freelist.
>
> Servers like FizzBuzz have very large messages and would benefit from reuse.
> Make the freelist larger, and add a goroutine that frees the freelist entries
> slowly over time, so that idle servers eventually release all freelist
> entries.

The first few words describe what the CL actually does. The rest of the
description talks about the problem being solved, why this is a good solution,
and a bit more information about the specific implementation.

### Refactoring

> Construct a Task with a TimeKeeper to use its TimeStr and Now methods.
>
> Add a Now method to Task, so the borglet() getter method can be removed (which
> was only used by OOMCandidate to call borglet's Now method). This replaces the
> methods on Borglet that delegate to a TimeKeeper.
>
> Allowing Tasks to supply Now is a step toward eliminating the dependency on
> Borglet. Eventually, collaborators that depend on getting Now from the Task
> should be changed to use a TimeKeeper directly, but this has been an
> accommodation to refactoring in small steps.
>
> Continuing the long-range goal of refactoring the Borglet Hierarchy.

The first line describes what the CL does and how this is a change from the
past. The rest of the description talks about the specific implementation, the
context of the CL, that the solution isn't ideal, and possible future direction.
It also explains *why* this change is being made.

### Small CL that needs some context

> Create a Python3 build rule for status.py.
>
> This allows consumers who are already using this as in Python3 to depend on a
> rule that is next to the original status build rule instead of somewhere in
> their own tree. It encourages new consumers to use Python3 if they can,
> instead of Python2, and significantly simplifies some automated build file
> refactoring tools being worked on currently.

The first sentence describes what's actually being done. The rest of the
description explains *why* the change is being made and gives the reviewer a lot
of context.

## Review the description before submitting the CL

CLs can undergo significant change during review. It can be worthwhile to review
a CL description before submitting the CL, to ensure that the description still
reflects what the CL does.

Next: [Small CLs](small-cls.md)

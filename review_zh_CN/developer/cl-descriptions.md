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

通常，CL 代码变更的第一个描述信息应该是一个完整的命令式语句。
比如：使用 "删除 FizzBuzz RPC 并使用新的系统替代它" 而不是 "将要删除 FizzBuzz RPC 并替换它"
步步过，其他描述信息不必是命令式的。

## Body is Informative 正文应该是信息充足的 {#informative}

代码变更描述信息的其他部分应该是信息充足的。可以简要的描述要解决的问题，并说明为什么这么做是最合理的。
如果解决方案有任何缺陷，都要在描述中提及。
必要的话，还需要包含 bug 的编号，测试结果，设计文档链接。

即便是很小的代码变更，至少也要包含变更点列表。

## Bad CL Descriptions 糟糕的代码变更描述 {#bad}

"Fix bug" 是无意义的描述。修改了什么杨的 bug？ 通过什么方法修复了这个 bug？

其他类似，无意义的代码变更描述：

- "Fix build."                        修复构建
- "Add patch."                        打补丁
- "Moving code from A to B."          把代码从 A 移动到 B
- "Phase 1."                          阶段 1
- "Add convenience functions."        添加好用的功能
- "kill weird URLs."                  干掉奇怪的 url 们

上面是一些真是的代码变更描述信息。开发人员认为自己提供了有用的信息，可是它们真的毫无意义。

## Good CL Descriptions 好的代码变更描述 {#good}

下面是一些好的代码变更描述示例.

### Functionality change 功能变更

> rpc: remove size limit on RPC server message freelist. 删除对 RPC 服务器消息空闲列表的大小限制。
>
> Servers like FizzBuzz have very large messages and would benefit from reuse.
> Make the freelist larger, and add a goroutine that frees the freelist entries
> slowly over time, so that idle servers eventually release all freelist
> entries.

第一行的几个单词描述了该代码变更做了什么。
剩下的描述信息谈论了：要解决的问题，为什么这是一个好的解决方案以及该代码实现的一些信息。

### Refactoring 代码重构

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

第一行描述了代码变更的目的以及跟旧代码的差异。
剩下的描述信息说明了具体实现方案，变更的上下文(背景)，修改方案并不理想，将来可能的修改方向。
它还说明了 `为什么` 进行此项修改。

### Small CL that needs some context

> Create a Python3 build rule for status.py.
>
> This allows consumers who are already using this as in Python3 to depend on a
> rule that is next to the original status build rule instead of somewhere in
> their own tree. It encourages new consumers to use Python3 if they can,
> instead of Python2, and significantly simplifies some automated build file
> refactoring tools being worked on currently.

第一行描述了正在做的变更内容。
其他部分解释了为什么做这中修改，并为代码审查者提供了很多背景(上下文)信息。

## Review the description before submitting the CL 提交(git推送)代码之前开发人员需要自查一遍描述信息

在代码审查期间，代码变更可能发生重大变更。
开发人员再次提交推送代码之前应该确认一下提交信息，以保证其正确地描述了变更内容。

Next: [Small CLs](small-cls.md)

# What to look for in a code review 代码变更寻求什么

注意：在考虑这些要点时，请始终牢记 [The Standard of Code Review](standard.md)

## Design 设计

代码审查中最重要的点是代码变更 CL 的总体设计。
代码变更中各个部分的交互是否有意义？
这些变更应该在当前 codebase 中，还是 code library 中国？
它与系统的其他部分是否集成良好？
现在是添加此功能的好时机吗？

## Functionality 功能方面

该代码变更是否满足开发人员的预期？开发人员打算为该代码的用户带来什么好处？
“用户”通常包含终端用户(当他们能感受到这种变化时，比如 UI 的变化) 和 开发者(不得不调用这些代码的人)。

通常，我们希望开发人员能够对代码变更进行很好的测试，以保证在进行代码审查时他们能够正确的工作。
然后，作为代码审查者，你仍然应该考虑边界情况，检查并发问题，尝试像用户一样思考，并且确保没有仅通过阅读代码就能发现的问题。

如果你想的话，你可以验证代码变更。
如果代码变更对终端用户有影响，比如 **UI change** ，审查代码变更的行为是很重要的。
仅仅通过阅读代码很难理解某些变更将如何影响用户。
对于这些变更，如果不方便自己验证，可以让开发人员进行功能演示。

另一个考虑功能特性的点是：代码变更中是否有可能引起死锁或者竞争条件的并发问题。
仅仅通过运行代码很难发现这类问题，通常需要有人（开发人员和代码审查者）仔细考虑，以确保不会引入这类问题。
（请注意，这也是在可能出现竞争条件或死锁的情况下不使用并发模型的一个很好的理由，这会使得进行代码审查或理解代码非常困难。）

## Complexity 复杂性

代码变更是否过于复杂？
在代码变更的各个方面进行审查：个别代码行实现的是否太复杂？函数是否太复杂？类是否太复杂？
代码太复杂通常表示代码阅读者难以快速理解代码。这也意味着开发人员调用或者修改这些代码时很容易引入bug。

一种特殊的复杂性是过度设计，即开发人员使得代码过于通用，或者增加了系统当前并不需要的功能。
审查者应该特别警惕过度设计。
过滤开发人员去解决已知的当前需要解决的问题，而不是开发人员推测的将来可能需要解决的问题。
将来的问题将来解决。

## Tests 测试

要有单元测试，集成测试，端到端的测试。
根据代码变更情况进行测试。
一般来讲，代码修改和测试应该在同一个代码变更中，除非为了解决紧急情况 [emergency](../emergencies.md).

保证代码变更中的测试是正确的、合理的、有用的。
测试不会自我测试，我们很少为测试编写测试-人来保证测试的有效性。

代码被破坏时，测试会失败吗？代码变更会导致测试误报吗？每个测试都会做出简单而有用的断言吗？
不同的测试方法是否恰当地隔离。

记住，测试也是要维护地代码。不要因为他们不是发布包地一部分，而接受他们地复杂性。

## Naming 命名

开发人员是否为变量、方法、类等等选择了合适的名字？
一个好的名字应该能表明自己是什么或者要做什么，而又不会因为太长导致难以阅读。

## Comments 注释

开发人员是否书写了清晰的注释？
注释都是必要的吗？通常，注释应该解释代码为什么存在，而不是说明代码在做什么。
如果代码本身不能清晰的自我说明，代码就应该写的再简单一点。
当前也有一些例外的情况（例如，正则表达式和复杂算法通常需要在注释中说明他们在做什么）
但大多数注释是针对代码本身可能无法包含的信息，例如决定背后的原因。

修改代码的时候也要检查之前的代码注释。可能某个 TODO 现在可以移除了，可能建议不要进行这块代码的修改。

记住，注释不同于类，模块，函数的文档，文档应该说明一段代码的用途，应该如何使用，以及使用时的行为。

## Style 代码风格

We have [style guides](http://google.github.io/styleguide/) at Google for all
of our major languages, and even for most of the minor languages. Make sure the
CL follows the appropriate style guides.

If you want to improve some style point that isn't in the style guide, prefix
your comment with "Nit:" to let the developer know that it's a nitpick that you
think would improve the code but isn't mandatory. Don't block CLs from being
submitted based only on personal style preferences.

The author of the CL should not include major style changes combined with other
changes. It makes it hard to see what is being changed in the CL, makes merges
and rollbacks more complex, and causes other problems. For example, if the
author wants to reformat the whole file, have them send you just the
reformatting as one CL, and then send another CL with their functional changes
after that.

## Documentation

If a CL changes how users build, test, interact with, or release code, check to
see that it also updates associated documentation, including
READMEs, g3doc pages, and any generated
reference docs. If the CL deletes or deprecates code, consider whether the
documentation should also be deleted.
If documentation is
missing, ask for it.

## Every Line {#every_line}

Look at *every* line of code that you have been assigned to review. Some things
like data files, generated code, or large data structures you can scan over
sometimes, but don't scan over a human-written class, function, or block of code
and assume that what's inside of it is okay. Obviously some code deserves more
careful scrutiny than other code&mdash;that's a judgment call that you have to
make&mdash;but you should at least be sure that you *understand* what all the
code is doing.

If it's too hard for you to read the code and this is slowing down the review,
then you should let the developer know that
and wait for them to clarify it before you try to review it. At Google, we hire
great software engineers, and you are one of them. If you can't understand the
code, it's very likely that other developers won't either. So you're also
helping future developers understand this code, when you ask the developer to
clarify it.

If you understand the code but you don't feel qualified to do some part of the
review, make sure there is a reviewer on the CL who is qualified, particularly
for complex issues such as security, concurrency, accessibility,
internationalization, etc.

## Context

It is often helpful to look at the CL in a broad context. Usually the code
review tool will only show you a few lines of code around the parts that are
being changed. Sometimes you have to look at the whole file to be sure that the
change actually makes sense. For example, you might see only four new lines
being added, but when you look at the whole file, you see those four lines are
in a 50-line method that now really needs to be broken up into smaller methods.

It's also useful to think about the CL in the context of the system as a whole.
Is this CL improving the code health of the system or is it making the whole
system more complex, less tested, etc.? **Don't accept CLs that degrade the code
health of the system.** Most systems become complex through many small changes
that add up, so it's important to prevent even small complexities in new
changes.

## Good Things {#good_things}

If you see something nice in the CL, tell the developer, especially when they
addressed one of your comments in a great way. Code reviews often just focus on
mistakes, but they should offer encouragement and appreciation for good
practices, as well. It’s sometimes even more valuable, in terms of mentoring, to
tell a developer what they did right than to tell them what they did wrong.

## Summary

In doing a code review, you should make sure that:

-   The code is well-designed.
-   The functionality is good for the users of the code.
-   Any UI changes are sensible and look good.
-   Any parallel programming is done safely.
-   The code isn't more complex than it needs to be.
-   The developer isn't implementing things they *might* need in the future but
    don't know they need now.
-   Code has appropriate unit tests.
-   Tests are well-designed.
-   The developer used clear names for everything.
-   Comments are clear and useful, and mostly explain *why* instead of *what*.
-   Code is appropriately documented (generally in g3doc).
-   The code conforms to our style guides.

Make sure to review **every line** of code you've been asked to review, look at
the **context**, make sure you're **improving code health**, and compliment
developers on **good things** that they do.

Next: [Navigating a CL in Review](navigate.md)

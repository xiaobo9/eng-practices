# How to write code review comments 怎么编写代码审查评论

## Summary 简介

- Be kind. 友善一些。
- Explain your reasoning. 说明你地理由。
- 给出明确地方向？仅仅指出问题，让开发人员决定怎么做？ 权衡一下。
- 鼓励开发人员简化代码或者增加代码注释，而不是仅向你个人解释代码的复杂性。

## Courtesy 礼貌

对代码被审查的开发人员应该礼貌和尊重，审查意见也要清楚且有帮助。
代码审查意见只针对代码而不对人。
评论意见会会让开发人员沮丧或者引起争论的时候，一定要遵循这些意见。

例如：

糟糕的例子：“在并发显然没有好处的情况下，为什么‘你’要在这里使用多线程”

好的例子：“这里的并发模型将增加系统的复杂性，而我没有看出来任何实际的性能优势。
因为没有性能方面的优势，所以这块代码最好使用单线程。”

## Explain Why 说明为什么 {#why}

从上面好的例子，你应该注意到一件事情：你需要帮开发人员了解你给出评论意见的原因。
并不总是需要你在代码评论中包含此信息，但有时需要对你的意图、你遵循的最佳实践或你的建议将如何改善代码运行状况给出更多的解释。

## Giving Guidance 指导 {#guidance}

**通常，修复代码变更中的缺陷是开发人员而不是审查者的责任。** 你不需为解决方案做详细设计，或者帮开发人员写代码。

但是，这并不意味着审查者不应该做出帮助。你需要在指出问题和提供直接的知道之间做出权衡。
指出问题并让开发人员做决定可以帮助开发人员学习，然后使得代码审查越来越容易。
而且开发人员可能给出更好的解决方案，因为开发人员比审查者更接近这部分代码。

但是，有时，直接的指导，建议甚至代码将更有帮助。

* 代码审查的主要目标是使得代码变更尽可能地好
* 代码审查的第二个目标是提高开发人员的技能，然后他们的代码需要的审查就可以越来越少

## Accepting Explanations 接受解释 {#explanations}

如果你要求开发人员解释一段你不理解的代码，通常使得他们把“代码重构的更清晰” **。
有时，在代码中添加注释也是一种适当的响应，只要它不只是解释过于复杂的代码即可。

**仅在代码审查工具中编写的说明对将来的代码阅读者毫无意义。**
仅在某些情况下，比如，这段你不熟悉的代码，开发人员解释的内容，将来的阅读者是了解的，开发人员在审查工具中的解释说明是可接受的，这时候也就不必要求开发人员在代码中做出解释。

Next: [Handling Pushback in Code Reviews](pushback.md)

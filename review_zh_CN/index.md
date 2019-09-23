# 代码审查 开发人员指南

## 简介 {#intro}

代码审查是非代码作者检查代码的一个过程。

在 google，我们通过代码审查来控制代码和产品的质量

本文档是 google 代码审查过程和原则的规范描述

本页会简单介绍我们代码审查的过程。后面将有两篇文章详细表述：

- **[How To Do A Code Review](reviewer/)**: 一份针对代码审查者的详细资料
- **[The CL Author's Guide](developer/)**: 一份针对要被审查代码的作者的详细文档。

## 代码审查者们要探寻什么? {#look_for}

代码审查者们要着眼于下面这些内容:

- **Design**: 设计方面，代码是否经过精心设计并适合你的系统？
- **Functionality**: 功能方面，代码是否符合作者的预期意图？代码是否满足终端用户的功能预期
- **Complexity**: 复杂度方面，代码逻辑是否可以更简单一些？将来，其他开发人员是否可以轻松地理解并使用这些代码？
- **Tests**: 测试方面，代码是否具有正确且设计良好的自动化测试？
- **Naming**: 命名方面，开发人员是否选择了合适的明确的变量名，类名，方法名等等？
- *Comments**: 注释方面，注释是否明晰且有用？
- **Style**: 代码是否满足 code style 的要求 [style guides](http://google.github.io/styleguide/)?
- **Documentation**: 开发人员是否更新了相关文档？

See **[How To Do A Code Review](reviewer/)** for more information.

### 选择最佳的代码审查者 {#best_reviewers}

通常，你需要选择能在合理的时间内响应你的审查请求的代码审查者。

他们有能力对你的代码给与深入并且正确的审查意见。所以，有时候需要不同的人来审查代码变更的不同部分。

如果理想的审查者无暇处理你的审查请求，也应该在审查请求中 @ 他们一下。

### In-Person Reviews {#in_person}

如果你和一个有代码审查资格的人一起结对编程实现了一段代码，那么这段代码可以认为是被审查过的。

You can also do in-person code reviews where the reviewer asks questions and the
developer of the change speaks only when spoken to.

## See Also {#seealso}

- [How To Do A Code Review](reviewer/): 一份针对代码审查者的详细资料
- [The CL Author's Guide](developer/): 一份针对要被审查代码的作者的详细文档。

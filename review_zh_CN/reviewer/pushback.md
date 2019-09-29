# Handling pushback in code reviews 处理代码审查中的反弹

有时开发人员会拒绝接受代码评论。他们要么不同意你的建议，要么抱怨你的审查过于严格。

## Who is right? 谁是正确的？ {#who_is_right}

如果开发人员不同意你的审查意见，先花点时间考虑一下他们是不是对的。
通常，他们比你更接近这些代码，因此实际上，他们可能对代码的某些方面有更好的了解。
他们的论点有意义吗？这有助于提升代码健康状况吗？
如果是的话，让他们知道他们是对的，并关闭问题评论。

但是，开发人员并不总是对的。这时候，审查者应该进一步解释为什么认为自己的审查意见是正确的。
好的解释即说明你理解了开发人员的回复，也说明了为什么代码应该被修正。

In particular, when the reviewer believes their suggestion will improve code
health, they should continue to advocate for the change, if they believe the
resulting code quality improvement justifies the additional work requested.
**Improving code health tends to happen in small steps.**

有时，在审查意见被采纳之前，需要经过多轮审查意见的讨论。
请确保始终保持[polite 礼貌](comments.md#courtesy)，并让开发人员了解你看了他们的回复，但是你并不同意。

## Upsetting Developers {#upsetting_developers}

Reviewers sometimes believe that the developer will be upset if the reviewer
insists on an improvement. Sometimes developers do become upset, but it is
usually brief and they become very thankful later that you helped them improve
the quality of their code. Usually, if you are [polite](comments.md#courtesy) in
your comments, developers actually don't become upset at all, and the worry is
just in the reviewer's mind. Upsets are usually more about
[the way comments are written](comments.md#courtesy) than about the reviewer's
insistence on code quality.

## Cleaning It Up Later 不要延迟清洁代码 {#later}

A common source of push back is that developers (understandably) want to get
things done. They don't want to go through another round of review just to get
this CL in. So they say they will clean something up in a later CL, and thus you
should LGTM *this* CL now. Some developers are very good about this, and will
immediately write a follow-up CL that fixes the issue. However, experience shows
that as more time passes after a developer writes the original CL, the less
likely this clean up is to happen. In fact, usually unless the developer does
the clean up *immediately* after the present CL, it never happens. This isn't
because developers are irresponsible, but because they have a lot of work to do
and the cleanup gets lost or forgotten in the press of other work. Thus, it is
usually best to insist that the developer clean up their CL *now*, before the
code is in the codebase and "done." Letting people "clean things up later" is a
common way for codebases to degenerate.

If a CL introduces new complexity, it must be cleaned up before submission
unless it is an [emergency](../emergencies.md). If the CL exposes surrounding
problems and they can't be addressed right now, the developer should file a bug
for the cleanup and assign it to themselves so that it doesn't get lost. They
can optionally also write a TODO comment in the code that references the filed
bug.

## General Complaints About Strictness {#strictness}

If you previously had fairly lax code reviews and you switch to having strict
reviews, some developers will complain very loudly. Improving the
[speed](speed.md) of your code reviews usually causes these complaints to fade
away.

Sometimes it can take months for these complaints to fade away, but eventually
developers tend to see the value of strict code reviews as they see what great
code they help generate. Sometimes the loudest protesters even become your
strongest supporters once something happens that causes them to really see the
value you're adding by being strict.

## Resolving Conflicts {#conflicts}

If you are following all of the above but you still encounter a conflict between
yourself and a developer that can't be resolved, see
[The Standard of Code Review](standard.md) for guidelines and principles that
can help resolve the conflict.

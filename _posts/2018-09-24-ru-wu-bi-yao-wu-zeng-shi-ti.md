---
layout: bigword
title: 如无必要，勿增实体
dec: 如无必要，勿增实体
excerpt: 我们相信牛顿定律的根基是什么呢？是奥卡姆剃刀，是我们觉得这个世界没那么复杂，当然，往往他确实没那么复杂，那个创造者制造的世界的规律就正好跟人希望的一样，是简单的，是有数学美感的。
category: think
---

今天看到一个视频，让我想到了一些曾经思考过的问题，可能称为xx观的还不能非常完备，但是也记录一下备忘。

虽然这个事情的思考过程不是如此，但是我想从简到难的叙述这个事情。记得高中时候我们的物理老师非常好，是个比较理性的老师，他在给我们讲变速运动和圆周运动的时候讲到如何近似为匀速直线运动的时候说道“这时候物理学家就要不讲理了，我们需要做一个近似”这时候我还没觉得这个近似有什么不妥，甚至觉得非常合理，世界中不是基本各种物理量都是连续分布的么，当然在很接近匀速直线的时候就可以使用匀速直线来计算了。直到我在学大一物理的时候做错了一道题。

这道题的大致意思是，一个均匀带电荷+Q的无厚度圆盘，对于在其中心的电荷量为+q的质点的斥力为多少？这个题是要列出每个圆盘半径位置对于+q的斥力，并在圆盘半径上进行积分，最后取预设的+q到圆盘高度的极限到0，这样会得到一个常数。但是，当时我就抖了一个激灵，因为当时感觉上不会造出不连续的场，而且+q已经无限接近圆盘中心了，如果我把它放在圆盘中心呢，所有的力都对称抵消了，那么答案就是0。后来想想确实这个结论很多地方都是不值得推敲的。联想到之前学的一些物理近似，我发现我并不能找到一种判定标准，什么情况下是可以近似的，什么情况下又不能。

上面的例子是我真实遇到的，也是引起我开始思考这个问题的引子。如果你还认为上面的观点是可以轻松区分的，那么我接下来讲的一个“不合理证明”应该能够给你一些更深入的启发，这也是我今天看到这个视频之后的思考。下面将证明的是自然数的和是-1/12，如果你是见过这个结论的，这里只是举一个例子，也不是非常想讨论这个证明方法的问题。

```
S := 1 + 2 + 3 + ...
S1 := 1 - 1 + 1 - 1 + ...
S1 = 1/2 (如果这个结论不能认可，那么这里仅保留>=0, <=1 的不等式，一样能推出不可思议的结论)
S2 := 1 - 2 + 3 - 4 + ...

2 * S2 = 1 - 2 + 3 - 4 + ... （接下行）
           + 1 - 2 + 3 + ... （对应位置加和）
       = 1 - 1 + 1 - 1
       = S1
       = 1/2

S - S2 = 4 (1 + 2 + 3 + ...)
       = 4 * S

S = -1/12   
 
```

这是怎么回事，我觉得在刚看到这个结论的时候，我们应该都会对这个结论产生反感，这种答案怎么可能正确，正数相加怎么可能得到一个负数？于是我们去查找这个证明方法中有什么漏洞，你可能发现了比如等式两边同时消去一个正无穷会不会有问题，或者不收敛的级数是否可以错位相加等等。（那么级数理论出问题了么，我个人觉得这个问题还是出在对不收敛的级数进行错位计算的问题，这个trick让这个级数有了上下界，不过这篇文章不是主要讨论这个问题，在这里仅仅举例）总之我们会各种怀疑这个推理的方法哪里出了问题。

但是，如果我告诉你这就是弦论中使用的中间结论呢？也就是说这个结论其实没有错，在某些情况下确实有用，而且已经被用于计算，甚至被之后的实验所证实。那么我们可能就要重新审视这个结果了，借用视频中的解释是“你之所以不能理解这个答案，是因为你一直想把这个序列求和停下来，如果你停下来他就不是这个数列了，也就理解不了这最终的结果”，可能现在我们想的更多的是，这个结果到底代表着什么意思。从前到后我的思想上确实发生了一些变化，这不禁让我反思到底什么是可近似的结果，怎样产生的理论是有效的？

以前认为，从真实的实验结果出发，使用科学的推理得到的结论就是有效的。这也是我们授课的顺序，其实真实的顺序却不是这样，我们提出理论，这个理论真正能够被实践验证，我们反向去思考他的道理，给出了这个理论的推理，并把这个推理写在教科书上，并由此引出这个理论。我们可能能判断一个新出现的理论是否是错误的，但是很难仅从推理过程得知他是否正确。实践是检验真理的唯一标准，这我们早就了解过了。下午跟同学聊天的时候还说到这个事情。“飞机是如何飞起来的呢，不是因为空气动力学原理，而是从人类不断的失败实验中总结出来的。”

如果只有实践才能检验真理，那么紧接着就会带来一个新的问题，实践是无法穷尽的，我们如何确保一个理论真的成立，我们上中学时在实验室中用各种方法多次验证了牛顿第二定律的真实性，就算我们所有的同学的实验、所有历史上所有科学家所有学生和爱好者的实验，也不能穷尽，因为他的作用空间是无限的连续，甚至由于人类所处世界的局限性，有些实验也是我们无法做出的。这也是我们已经被用了这么长时间的牛顿定律最终被相对论修正的原因。这有些不可知论的节奏，注意我们讨论的是实践如何检验真理的问题，如果真理不能被穷尽检验，那么它就是在某种情况下成立的，这种结论我们是否敢用呢？

最终引出文章题目，其实我们相信牛顿定律的根基是什么呢？是奥卡姆剃刀，是我们觉得这个世界没那么复杂，当然，往往他确实没那么复杂，那个创造者制造的世界的规律就正好跟人希望的一样，是简单的，是有数学美感的（有时候真觉得唯心主义有那么一点道理，确实神合的地方很多）。因为我们觉得对于某一个定值设定特殊法则是非常麻烦的，是有悖人类尝试的，我们就用简单的几个值的实践去检验了真理，并对此深信不疑。记得大三交换的时候科学技术史老师说过，人类科学技术的最大成果其实是研究出了一套研究科学的方法，那就是 问题——理论——预测——验证，可见这里一是说明了“实践是检验真理的唯一标准”，我们确实没有其他方法；二是说明了，我们验证理论预测的一部分就可以，并不是要穷举所有可能，理论其他输入靠奥卡姆剃刀保证。

最后说一句题外话，奥卡姆剃刀是事实吗？它本身也只是人类对于自然规律的总结，想证明他自己还是要用到它自己。说白了这是一种感觉，是无法被证实的（甚至像相对论——经典力学这个还是一个反例），是人类祈求造物主的一种怜悯，我们希望它这样，也认为它就是这样的，但是如果不然我们没有任何办法。

之前看到知乎上一篇回答说的世界其实是是一个上帝造的世界，人类生活其中，每天被人类科技发展而苦于制造更严密的补丁法则和更广远的太空。想到这里，我觉得“如无必要，勿增实体”可能更是要对他们说的吧。


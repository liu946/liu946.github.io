---
layout: plain
title: AI爆炸了，技术准备好了吗？
dec: AI爆炸了，技术准备好了吗？
excerpt: 当人们渐渐清楚的认识了AI的能力之后这波“AI时代“可能就会过去了吧。
category: think
---

### 引子

首先描述一下我目前在实习的一家NLP技术输出2b的创业公司的一些经历，以支持我之后的判断和思考。

公司成立与2017年8月，至今已经一年有余。从公司成立之初开始，就开始准备走高科技道路，并与高校实验室合作，拿到了独家合作和老师的信任，与高校合作，这可能是目前AI创业的主要方式，至少大部分的AI创业公司都是从学校走出来的。公司CEO是大我8届的师兄，腾讯3年工作经验，后又有几次创业经验，曾经也参与创业了一家百余人的公司，三年时间将一个公司做起来也算是不易，同时积累了很多创业的经验和伙伴。CTO是微软和阿里待过多年的资深NLP工程师。公司这边可能比较严重的问题是成员技术水平不足，大多是廉价招收的刚刚毕业的本科生，并没有什么工作经验，当然也没有AI的经验。公司的目标业务是NLP技术的输出，做2b，接到的单子确实不少，数据创业公司、政府部门、国企等等。CEO经常说我们是凑足了天时地利人和了，我觉得也是吧，起码能和实验室合作对接实验室的名声和技术确实是占足了便宜了。

18年5月我加入公司，实际公司才真正接手第一个NLP项目，是给一个数据公司做论文的分类和关键词抽取。由于我们的经验不足，前期乐观地将工期定为半个月，甲方提供数据存在大量问题，导致最后模型效果和我们验证的完全不同。这个项目也是一拖再拖，一直拖到了现在（10月底），当然不能说半个月的事情我们进行了4个半月，期间还有很多其他项目也在忙。但是从中可以看出，这种非确定性编程的需求确定和交付之间是存在大量问题的，起码对于我们来说是不成熟的。

在之后的对接一个国企的实体识别项目中（无任何数据），每此训练模型已经达到95%左右，但是实际测试确实准确率和召回率都仅仅在50%左右。没有数据如何做效果好机器学习呢？这可能是一个巨大的难题，反正目前的机器学习研究是不能达到的。反过来说，这在理论上都有一定的难度，你不告诉机器如何去做机器怎么可能自己就会了呢？我们目前采用的是一种远程监督的方法，使用一些规则去回标数据，模型就是因为比规则复杂才能达到更好的效果，但是让模型去学习规则，引入的错误就会大大增加（顺便一说，我们这里的回标程序的准确率只有30%）。

可能是我们的系统磨炼的还不够充分吧，毕竟第一次做这个事情，结果可想而知。甲方看到结果之后对结果很不满意，打回重做，而且这个项目要求还很高时间很紧，每周都要出下一个模块的demo，但是上一个模块又返工重做了，这个恶性循环导致我们新的模块也做不好，旧模块也优化不好，大家都非常疲惫。

### NLP的2b公司，成立吗？

现在的时代是否可以建立AI的2b公司呢？我们可以先从理论上来分析一下。

2b公司，尤其是这种技术型的，其实生存空间不大，只能服务于那些需要这个高科技，而且自己不会，而且又钱买你的产品，又没有那么大的体量可以自己做的，这样就排除了懂技术的公司，也排除了小公司，大公司，只剩下那些中档公司，自己做花费太多，让你做给你钱花费少。那为什么花更少的钱你能做呢？因为公司做过很多，我们不需要那么多成本做这个事情。也就是说我们赚的是省出来的钱，是复用的钱。

首先2b公司是面向业务拿钱的，也就是这个公司本来就应该开始就盈利，不存在2c“前期培养用户”这个过程，干一份工作那一份钱。所以现在能够盈利也并没有什么特别的，只是我们见过的2c的点子公司太多了，拿来了一个不应比较的对象而已。现在我们能盈利是不是说明这种模式就没有问题，只要一直做下去，我们挣的钱能养活我们自己这个公司就不会垮呢？我认为现在我们的盈利之中存在着问题，首先我们的成果并不能使客户满意，往往是做不到，给客户一个半成品demo，性能上还差得很远，但是我们这边再提高一些，同时客户那边的心里预期也越来越低，最后大家实在是想结束这个事情了，match到了一起，甲方不得已同意了这个demo级别的，而且效果远不如自己想像的那个结果。虽然这次甲方付了钱，这个合作可能就没法进行下去了，甲方对于AI的期待也回到了冰点，可能他们再也不会尝试使用AI做什么事情了。所以目前公司的项目合作并不是良性的，是持续不了的。

如果我们用更多的人力，顾更好的技术人员，使用更好的技术呢？是否可以达到甲方的标准。这个我就不做过多的论述了，可能在部分任务上可以达到，但是需要大量的人力和财力成本，那么我们现在的支出可能就养活不了这些人了。说到这里，我觉得我可以描述的一个可能失败的场景出现了，为什么天时地利人和不能成功呢？因为这个产业链还没有准备好，其中还没有机会，你的复用性不能支持养活你的员工，如果强行雇佣便宜的员工，那么就会出现现在的让员工累死，让甲方失望的恶性循环。

对比语音识别（讯飞）和人脸识别（face++）的两家公司，我们或许可以看出端倪。这两个公司的核心是感知任务，理论上比我们现在做的认知任务要简单一些，因此他们已经达到了能成为2b公司的能养活员工的复用性。那么这两个公司的产品到底达到如何的准确性呢？几乎100%，而且这带来的另一个好处是，简单的领域迁移也不会过多影响性能。相比之下我们的任务呢？首先迁移领域往往会导致一些任务根本不能0语料做，比如某领域的实体识别任务，即使有方法迁移，之前的语料中也没有标记过新领域的新实体。一些指标本身就不高的任务会因为领域迁移而导致性能的直线下滑。感知可能准备好了，认知远远没到可用。认知任务上实验室和工业界可能差距更大，不是实验室90%工业就可能90%，因为实际场景太复杂。想想我们实际任务，你想让模型通过一个只会30%的老师那里学到知识，并且应用于另一个领域答对90%的题目呢，确实不切实际。

### AI时代是怎么来的？

上次与CEO聊，说现在AI时代来了，再不创业就过去了。想起来1年之前车老师也说过这样的话。说实话我内心还是认同这个事情的，但是最近遇到的这些事情不得不让我重新思考，AI时代是怎么来的？

我仔细想了一下，主要有两点。一个是深度学习引爆了科研圈，这个确实让我们都认为AI的时代到来了，因为我们太熟悉这个圈子。但是刚才也说了，实际场景和实验室的差距太大。使得我们不得不重新思考这个问题，深度学习能为工业界带来什么，深度学习让我们的模型从80%到90%，但是它如何解决模型90%但是实际效果50%的问题呢？我想工业界NLP可能主要不是要解决模型问题，深度学习对模型的提升其实没有对工业界产生多大的影响。模型提升没有带来可观的收益，该不能用的任务，好像还是不能用。

第二点就是“Alpha Go”这件事情把大众的视线引导到AI了。这也就解释了为什么我们现在有这么多的业务可以接，“Alpha Go”起码起到了炸粘子的作用，这让我们大一的同学进来就开始说想加入实验室做AI了。而且旁观者往往不能估计任务难度，他们认为对于自己来说“围棋”很难，“分词”简单，就觉得AI都能下围棋了，那么分个词肯定没啥问题。人们错误理解了AI的能力，这也就说明了我们对接的客户为什么会一次次地对AI降低期待，因为有些AI准备好了，并不是所有都准备好了。当人们渐渐清楚的认识了AI的能力之后这波“AI时代“可能就会过去了吧。

下次AI爆发是什么时候呢？希望那时候技术已经准备好了。



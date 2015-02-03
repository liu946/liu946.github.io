---
layout: plain
title: 初识NoSQL 快速认识NoSQL数据库
dec: 快速认识NoSQL数据库
excerpt:  做了一年的大一年度项目了，对于关系型数据库结构还是有些了解了，有的时候还是觉得这种二维表不是很顺手。在看过一篇文章之后，对NoSQL有了初步的了解，（https://keen.io/blog/53958349217/analytics-for-hackers-how-to-think-about-e
category: tech
exurl: http://www.cnblogs.com/liu946/p/3932565.html
---
<div id="cnblogs_post_body"><p><span style="font-family: Microsoft YaHei;">做了一年的大一年度项目了，对于关系型数据库结构还是有些了解了，有的时候还是觉得这种二维表不是很顺手。在看过一篇文章之后，对NoSQL有了初步的了解，（https://keen.io/blog/53958349217/analytics-for-hackers-how-to-think-about-event-data）。这边文章写的很好，确实写出来了在实际情况下NoSQL的&ldquo;用武之地&rdquo;，而且用了MineCraft作分析，但是也许不够全面。比如文章中只是提到了，entity数据用关系型怎么存，event数据用NoSQL怎么存，我想借我这篇文章，来分析一下event类型的数据原始的关系型数据库是怎样存数据的，然后再对这两种储存方式做一种对比，算是对原文都一种补充吧。</span><br /><br /><span style="font-family: Microsoft YaHei;">对于这种死亡事件，有这样的两条数据，一个是关于creeper的爆炸，一种是掉进岩浆。如果必须用关系型二维表数据库，我会这样存储。（如果您还不知道是什么样的数据，可以先看之后的NoSQL储存方法，那样看起来更清楚。）</span></p>
<p><br /><strong><span style="font-family: Microsoft YaHei;">这种情况的数据可以说是数据库设计中比较复杂的一种情况了，因为它包含两种情况（当然不止这两种情况，那么就会产生更多的结构），不同情况的数据表结构是不同的，这非常麻烦。我们一般的解决方案是设计四个表格，利用关系型数据库的关系性。设计如下四张表格。（在这里我就简写了）</span></strong></p>
<p><br /><span style="font-family: Microsoft YaHei;">第一张表</span></p>
<div class="cnblogs_code">
<pre><span style="font-family: Microsoft YaHei;">    id <span style="color: #008000;">#</span><span style="color: #008000;">首先用于关联，主表需要有个id，这个倒不是什么区别，因为NoSQL一般也会有个_id的预设</span>
    timestamp <span style="color: #008000;">#</span><span style="color: #008000;">所有共同部分就可以存在一张表中。</span>
<span style="color: #000000;">    cause
    player_UID
    player_experience
    player_age        </span><span style="color: #008000;">#</span><span style="color: #008000;">对于player_inveneory_id 因为这是一个可以任意长度的数组，又只能保存在另一个表中了</span></span></pre>
</div>
<p><span style="font-family: Microsoft YaHei;">第二张表（用于保存creeper死亡方式的死亡事件的）</span></p>
<div class="cnblogs_code">
<pre><span style="font-family: Microsoft YaHei;">    id <span style="color: #008000;">#</span><span style="color: #008000;">这是这张表的id以后可以跟别的表格关联</span>
    mid <span style="color: #008000;">#</span><span style="color: #008000;">用于关联主表</span>
<span style="color: #000000;">    enemy_type
    enemy_power
    enemy_distance
    enemy_age</span></span></pre>
</div>
<p><span style="font-family: Microsoft YaHei;">第三张表（用于保存lava死亡方式的死亡事件的）</span></p>
<div class="cnblogs_code">
<pre><span style="font-family: Microsoft YaHei;">    id <span style="color: #008000;">#</span><span style="color: #008000;">这是这张表的id以后可以跟别的表格关联</span>
    mid <span style="color: #008000;">#</span><span style="color: #008000;">用于关联主表</span>
<span style="color: #000000;">    place_x
    place_y
    place_z</span></span></pre>
</div>
<p><span style="font-family: Microsoft YaHei;">&nbsp;</span></p>
<p><span style="font-family: Microsoft YaHei;">第四张表（用于保存player_inveneory）</span></p>
<div class="cnblogs_code">
<pre><span style="font-family: Microsoft YaHei;">    id <span style="color: #008000;">#</span><span style="color: #008000;">这是这张表的id以后可以跟别的表格关联</span>
    mid <span style="color: #008000;">#</span><span style="color: #008000;">用于关联主表</span>
    inveneory</span></pre>
</div>
<p><span style="font-family: Microsoft YaHei;">至此关系性数据库就将这种有不同结构的事件存放方式规定好了，接下来存放如下（我就不画表格了）</span></p>
<div class="cnblogs_code">
<pre><span style="font-family: Microsoft YaHei;">1<span style="color: #000000;">.
    id    timestamp                    cause        player_UID        player_experience    player_age
    </span>1     <span style="color: #800000;">"</span><span style="color: #800000;">2013-05-23T1:50:00-0600</span><span style="color: #800000;">"</span>    <span style="color: #800000;">"</span><span style="color: #800000;">creeper</span><span style="color: #800000;">"</span>    <span style="color: #800000;">"</span><span style="color: #800000;">99234890823</span><span style="color: #800000;">"</span>     8873729               228        
    2     <span style="color: #800000;">"</span><span style="color: #800000;">2013-05-24T23:25:00-0600</span><span style="color: #800000;">"</span>   <span style="color: #800000;">"</span><span style="color: #800000;">lava</span><span style="color: #800000;">"</span>      <span style="color: #800000;">"</span><span style="color: #800000;">99234890823</span><span style="color: #800000;">"</span>     88737                 22

2<span style="color: #000000;">.
    id    mid     enemy_type    enemy_power    enemy_distance    enemy_age
    </span>1     1       <span style="color: #800000;">"</span><span style="color: #800000;">creeper</span><span style="color: #800000;">"</span>     .887           3.34             .6677

3<span style="color: #000000;">.
    id    mid    place_x    place_y    place_z
    </span>1     2      45.366     -13.333    -39.288

4<span style="color: #000000;">.
    id    mid    inveneory
    </span>1     1     <span style="color: #800000;">"</span><span style="color: #800000;">diamend sword</span><span style="color: #800000;">"</span>
    2     1     <span style="color: #800000;">"</span><span style="color: #800000;">torches</span><span style="color: #800000;">"</span>
    3     2     <span style="color: #800000;">"</span><span style="color: #800000;">stone</span><span style="color: #800000;">"</span></span></pre>
</div>
<p><span style="font-family: Microsoft YaHei;">&nbsp;至此，我们就用关系性数据库将这两个事件数据存下了。（好麻烦是吧！）</span><br /><br /><strong><span style="font-family: Microsoft YaHei;">我们再看NoSQL的储存方法，因为每条数据并不受字段（列名）限制，完全可以直接保存，不用分表。（比如JSON格式）</span></strong></p>
<div class="cnblogs_code">
<pre><span style="font-family: Microsoft YaHei;"><span style="color: #008000;">#</span><span style="color: #008000;">第一条数据</span>
<span style="color: #000000;">{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">timestamp</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2013-05-23T1:50:00-0600</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">cause</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">creeper</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">enemy</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        </span><span style="color: #800000;">"</span><span style="color: #800000;">type</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">creeper</span><span style="color: #800000;">"</span>
        <span style="color: #800000;">"</span><span style="color: #800000;">power</span><span style="color: #800000;">"</span>: .887
        <span style="color: #800000;">"</span><span style="color: #800000;">distance_from_player</span><span style="color: #800000;">"</span>:3.34
        <span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>:.6677<span style="color: #000000;">
    },
    </span><span style="color: #800000;">"</span><span style="color: #800000;">player</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">UID</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">99234890823</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">experience</span><span style="color: #800000;">"</span>: 8873729<span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>: 228<span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">inveneory</span><span style="color: #800000;">"</span>:[<span style="color: #800000;">"</span><span style="color: #800000;">diamend sword</span><span style="color: #800000;">"</span>,<span style="color: #800000;">"</span><span style="color: #800000;">torches</span><span style="color: #800000;">"</span><span style="color: #000000;">]
    }
}
</span><span style="color: #008000;">#</span><span style="color: #008000;">第二条数据</span>
<span style="color: #000000;">{
    </span><span style="color: #800000;">"</span><span style="color: #800000;">timestamp</span><span style="color: #800000;">"</span>: <span style="color: #800000;">"</span><span style="color: #800000;">2013-05-24T23:25:00-0600</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">cause</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">lava</span><span style="color: #800000;">"</span><span style="color: #000000;">,
    </span><span style="color: #800000;">"</span><span style="color: #800000;">place</span><span style="color: #800000;">"</span><span style="color: #000000;">:{
        x:</span>45.366<span style="color: #000000;">
        y:</span>-13.333<span style="color: #000000;">
        z:</span>-39.288<span style="color: #000000;">
    }
    </span><span style="color: #800000;">"</span><span style="color: #800000;">player</span><span style="color: #800000;">"</span><span style="color: #000000;">: {
        </span><span style="color: #800000;">"</span><span style="color: #800000;">UID</span><span style="color: #800000;">"</span>:<span style="color: #800000;">"</span><span style="color: #800000;">99234890823</span><span style="color: #800000;">"</span><span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">experience</span><span style="color: #800000;">"</span>: 88737<span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">age</span><span style="color: #800000;">"</span>: 22<span style="color: #000000;">,
        </span><span style="color: #800000;">"</span><span style="color: #800000;">inveneory</span><span style="color: #800000;">"</span>:[<span style="color: #800000;">"</span><span style="color: #800000;">stone</span><span style="color: #800000;">"</span><span style="color: #000000;">]
    }
}</span></span></pre>
</div>
<p><strong><span style="font-family: Microsoft YaHei;">下面我们分析NoSQL对这种数据存放方式的好处</span></strong><br /><span style="font-family: Microsoft YaHei;">1.首先是把分散的表结构整合了，让应该在一起的数据在一起了。</span><br /><span style="font-family: Microsoft YaHei;">这就像C语言中开多个数组储存还是用一个结构体数组的区别，将一些有关系的数据放在一起是人类一种自然的想法，当然会让人更加舒服，而且可以提高关联性和升级扩展的简易程度。</span><br /><br /><span style="font-family: Microsoft YaHei;">2.存放变得方便</span><br /><span style="font-family: Microsoft YaHei;">让我们来考虑有数据来了我们怎么储存。</span><br /><span style="font-family: Microsoft YaHei;">对于二维表数据库：</span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;1.分析数据是那种类型的</span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;2.存放主表数据，并获得返回id</span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;3.分支，加上主表id在不同情况下向lava或creeper表中存放数据</span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;4.开循环，向inveneory表中插入多条记录</span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;这还只是一个简述，还要考虑到对多个表格操作时的数据回滚问题，实际写起来30行左右，那么出错的可能就大大提高了。</span><br /><span style="font-family: Microsoft YaHei;">对于NoSQL类型</span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;一句话： </span></p>
<div class="cnblogs_code">
<pre><span style="font-family: Microsoft YaHei;"> insert(data);<span style="color: #008000;">#</span><span style="color: #008000;">伪码</span></span></pre>
</div>
<p>&nbsp;</p>
<p><span style="font-family: Microsoft YaHei;">其实想想便知道，取数据时原来的关系性数据库也会同样麻烦。</span><br /><br /><span style="font-family: Microsoft YaHei;">3.NoSQL更利于动态生成存放方式，灵活性高了很多，至少我们可以在存放数据的时候再设计数据库了（虽然可能预先设计会好一些）</span><br /><br /><br /><span style="font-family: Microsoft YaHei;">当然，如果存储的不是事件性或者类似此类数据那么就另当别论了，二维表还是有很多它本身的优势的。以上是我的一些个人的分析，当然还有很多普遍认同的观点，以下是一些普遍认同的关于两种数据库模式的优缺点分析，我也基本同意。</span><span style="font-family: Microsoft YaHei;">&nbsp;以下观点主要引自(http://blog.csdn.net/chenhuajie123/article/details/9374969)</span><br /><span style="font-family: Microsoft YaHei;">关系性优势：</span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;1.事务处理---保持数据的一致性；</span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;2.由于以标准化为前提，数据更新的开销很小（相同的字段基本上只有一处）；</span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;3.可以进行Join等复杂查询。</span><br /><span style="font-family: Microsoft YaHei;">关系型缺点：</span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;1. 扩展困难：由于存在类似Join这样多表查询机制，使得数据库在扩展方面很艰难; </span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;2. 读写慢：这种情况主要发生在数据量达到一定规模时由于关系型数据库的系统逻辑非常复杂，使得其非常容易发生死锁等的并发问题，所以导致其读写速度下滑非常严重; </span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;3. 成本高：企业级数据库的License价格很惊人，并且随着系统的规模，而不断上升; </span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;4. 有限的支撑容量：现有关系型解决方案还无法支撑Google这样海量的数据存储; </span><br /><span style="font-family: Microsoft YaHei;">NoSQL优势，主要体现在下面几点： </span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;1. 简单的扩展：典型例子是Cassandra，由于其架构是类似于经典的P2P，所以能通过轻松地添加新的节点来扩展这个集群; </span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;2. 快速的读写：主要例子有Redis，由于其逻辑简单，而且纯内存操作，使得其性能非常出色，单节点每秒可以处理超过10万次读写操作; </span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;3. 低廉的成本：这是大多数分布式数据库共有的特点，因为主要都是开源软件，没有昂贵的License成本; </span><br /><span style="font-family: Microsoft YaHei;">NoSQL数据库还存在着很多的不足，常见主要有下面这几个： </span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;1. 不提供对SQL的支持：如果不支持SQL这样的工业标准，将会对用户产生一定的学习和应用迁移成本; </span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;2. 支持的特性不够丰富：现有产品所提供的功能都比较有限，大多数NoSQL数据库都不支持事务，也不像MS SQL Server和Oracle那样能提供各种附加功能，比如BI和报表等; </span><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; &nbsp;3. 现有产品的不够成熟：大多数产品都还处于初创期，和关系型数据库几十年的完善不可同日而语; </span><br /><br /><span style="font-family: Microsoft YaHei;">&nbsp;&nbsp; <br /></span></p></div><div id="MySignature"></div>
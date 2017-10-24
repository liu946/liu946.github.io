---
layout: plain
title: Share Reading Reading "TACL16 LSTM's Syntax-Sensitive Dependencies Ability"
dec: 俱乐部分享。神经机器学习。
category: tech
---

以下是概览目录。

## NLP数据拓扑结构

- 词（误拼）
- 文本（文本分类、情感倾向、主题分类）
- 成对文本（翻译、含义推断）
- 上下文中的词（谓词识别，动词匹配，词性标注）
- 词之间的关系（主语检测，句法，语义角色标注）

## NLP特征

#### 直接可测特征

- 特征的可计数性，词袋特征。
- 单独词特征 （词，长度，字符特征，前后缀）
- 词元lemma和词干stem
- 词汇资源 （阴阳性、词型、格、体、数）
- 分布信息 
- 文本特征（词袋、权重）
- 上下文词特征（相对窗口、绝对位置）

#### 可推断的语言学特征

- 词性
- 短语结构树与依存句法树（句法关系，句法路径，深度，公共父节点）
- 语义信息：论元角色信息

#### 其他

- 组合特征
- N-gram特征
- 分布特征

## NLP特征案例

#### 语言识别

- 二元字母词袋特征


#### 主题分类

- 一、二元文法词袋特征
- lemma或词向量等分布特征
- 给词袋加权：安装信息量加权如tf-idf

#### 作者归属

- 词性一二三四元（pos），功能词（on of the）一二元、距离


#### 词性标注（POS-tag）

- 词本身：前后缀、词元、大词表频率
- 外部：周围单词及其前后缀、前面单词的预测结果
- *特征模板*

#### 命名实体识别（NER）

- 如何选择较大的上下文窗口？
	- 左边第一个谓词、右边第一个名词
- 依存分析器信息

#### 弧分解分析，句法分析（Parser)

- 利用头词、修饰词及其pos，窗口内单词及词性



<a class="media" href="/assets/file/NNMethodsForNLP_chap6-7.pdf">
<div style="font-size: 0">
  <script type="text/javascript" style="font-size: 0">
  document.ready = function() {  
        $('a.media').media({width:"100%", height:600});  
  };
 </script>
</div>

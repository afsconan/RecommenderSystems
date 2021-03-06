# 2002-Hybrid Recommender Systems Surveyand Experiments
# Abstract
介绍了推荐系统是干嘛的。  
现在的推荐系统为了效果，会综合使用很多技术，比如基于内容的推荐，协同推荐，基于领域知识的推荐，以及其他技术，并且会将这些技术混合使用。
本文介绍了一种基于领域知识和协同过滤的新的混合推荐系统Entree来推荐餐厅。更进一步的，我们将展示依据领域知识进行的打分能增强协同过滤的有效性。

# Introduction
推荐系统最初的定义:  
"people provide recommendations as inputs, which the system then aggregates and directs to appropriate recipients"  
现在变得广义了：  
用来描述这样一个系统，能够从一大堆的可选项中，为人提供个性化的推荐。并且已经是一些电商网站的必要组成部分。  
“个性化”，“有趣且有用”这两个词将推荐系统和搜索引擎区分开来。
搜索引擎更关心的是匹配，初代搜索引擎将精确匹配的信息返回，后来的google增加了信息的权威属性，从而返回更有用的信息。  
在推荐系统的研究一个常用的方式就是结合使用各种技术来达到效能的峰值。
所有已知的推荐技术，都各有优缺点，需要将他们结合，取长补短。
# 推荐技术
分类方式很多，通常依据为：
* 背景数据：在推荐处理流程启动前，系统能获取的数据
* 数据数据：用户输入系统的数据。
* 算法：结合背景数据和输入数据反馈结果。
在这个基础上，能将推荐系统分为五类：

## 协同推荐技术 Collaborative recommendation 
协同推荐技术时最著名和最多使用的技术。协同推荐技术会聚合用户对物品的打分或推荐意见，然后基于用户之间的比较来生成推荐项。  
一个协同推荐系统中，典型的UP是一个针对物品打分的形成向量。
打分有如下几种：打分的时间序列，二值化的打分（like/dislike)，实数值的打分。
推荐算法分类： Memory-Based ,Model-Based（NN，Latend Semantic，Bayesian Networks）
核心思想是 “people-to-people” 的相关性

## 基于人口统计学的推荐技术 Demographic recommender systems 
例 Grundy 的基于人与人之间的对话推荐书籍。  
基于人口统计学的推荐技术是“people-to-people” 的相关性的另一种体现，但它无需人对物品的历史评价信息。

## 基于内容的推荐 Content-based recommendation
基于内容的推荐是信息检索过滤的副产物。它根据用户过去喜欢的产品（本文统称为 item），为用户推荐和他过去喜欢的产品相似的产品。

[参考](https://blog.csdn.net/u011537073/article/details/54143441)

## 基于效用推荐（Utility-based Recommendation）
基于效用函数，及该物品的效用能慢足用户需求的打分。

## 基于知识的推荐
基于某一领域的一套规则，进行推荐。知道某些物品有什么特定用处。

# 比较各个推荐技术优缺点
## 推荐系统主要面对的问题
### 新用户：
因为推荐系统是根据人对物品的评分来进行的，当一个新用户加入时，缺乏其打分数据，很难对这个用户进行分类。

### 新物品：
相似的，一个新物品的加入，也缺乏人对该物品的打分。

###  "Outside the box" 推荐能力：
协同过滤的擅长处理该问题，基于内容推荐则不行 ： 如喜欢jazz 的人，大部分也喜欢classcial。那么会给喜欢jazz的人 推荐 classical。但是基于内容的话，这两者内容没有相似点，因而无法进行

###  "portfolio effect"
协同过滤和基于内容的过滤，都不能很好的处理该问题。描述如下：相同的新闻，在不同的媒体上会用相近的描述。但是看过一次之后的人，不会去看第二次。因而需要剔除这些相似度非常高的新闻。

### "灰山羊" 现象
一个用户和周围用户都不一样。在基于人口统计学的方法中，也会遇到这个情况，即哪些个性非常明显的用户。

## Ramp-up 问题
数据欺诈问题：一个推荐系统中的UP一旦建立，基本不变。这样，会存在一个延时，比如一个肉食主义者，突然变成了素食主义者，推荐系统还是会给他推荐牛扒，除非隔了很长一段时间。
collaborative, content-based and demographic 都有这个问题

相对的，Knowledge base 和 Utility-Based 的反馈都是实时的，不需要重新训练。所以可以处理这种问题。

## 协同推荐
当用户的点击非常稀疏时，很难计算用户和用户的相似度，因为只有很少的用户会对相同的物品打分。除非用户数量非常多。  
纯粹的协同推荐技术最适合于用户的兴趣和一小撮物品强相关的情况。  
存在问题的场景：
* 用户评价非常稀疏
* 当物品集合变换较快
* 当物品集很大，而用户兴趣很小的时候

有效的情况：
* 当一个用户和他相近用户兴趣相似的时候，最有效。


## 基于人口统计学的方法
不存在 新用户问题，因为不需要用户对物品的打分。  
主要原理，基于贝叶斯概率。

## 基内容的推荐
基于内容的推荐也有一个启动问题，需要足够多的打分作为基础。   
和协同过滤有相似的问题，受物品特征的影响非常强。（例如 打的标签或特征只有 演员，导演这些，那只能根据这些特征进行推荐）


## 基于效用函数推荐 Utility-Based 
使用效用函数 和 基于知识的推荐，之所以可以较好的避免稀疏和数据欺诈问题。因为他们不需要使用累计的统计学信息。  
一个好处是他可以混合使用许多不同的特征，例如推送计划，用户使用已经拥有该物品等。而不只是产品本身的特征。另外，这些非物品特性可能会有一些奇怪的效用。

基于效用的的推荐的可扩展性还体现在可以度量失败的程度。

## 基于知识的推荐 Knowledge Based
缺点：知识的获取。  
有如下三种类型的知识需要获取：  
* Catelog Knowledge: 需要推荐的物品属于什么类别。
* Functional Knowledge: 能够将用户的需求和物品的特征联系起来的功能函数。
* User Knowledge: 用户的特征，来自于人口统计学特征，或者其他的特征如爱好等。

优点：
提供临时的探索，需要的用户数少于效用函数。
不存在起始时，推荐效果差的问题。

推荐上限由知识领域决定




# 混合推荐系统
使用多种推荐技术或者其他技术来克服缺点，提高性能。
## Weighted
例子：
* P-Tagngo System 线性加权组合
* Pazzani’s 投票方式

优点：所有系统的能力都能被整合。  
缺点：有一个假设，即所有模型的结果大体上一致，但实际不是。

## Siwthcing
根据惩罚项，挑选推荐算法

## Mixed
将多种技术的结果混合发送，假设技术A覆盖了一小部分，技术B也覆盖了一小部分，最终的并集就大了。  
避免 new item 启动问题，因为混合的技术，能避免new item 问题

## Feature Combination
将协同过滤得到的信息作为特征 加入基于内容的技术中。

## 分层策略
第一层，比较粗糙的，第二层，比较精细的

## 特征扩充
使用前一种推荐算法的输出结果作为后一种推荐算法的输入特征。


## Meta-level
前一种推荐模型作为后一种模型的输入。
























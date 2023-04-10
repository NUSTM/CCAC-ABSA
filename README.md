# CCAC2023多领域多要素属性级情感分析评测

## 背景介绍

“第三届中国情感计算大会”（Chinese Conference on Affect Computing, CCAC 2023）将于2023年7月在陕西西安召开。CCAC聚焦情感计算处理的前沿研究，为传播情感计算最新的学术和技术成果提供交流平台。中国情感计算大会每年举办一次，现已成为自然语言处理、社会计算领域的重要学术活动。第三届中国情感计算大会（CCAC 2023）由中国中文信息学会情感计算专委会（筹）主办，西安交通大学承办。作为中国中文信息学会（国内一级学会）在情感计算领域的重要会议，CCAC聚焦于语言、语音、视觉、生理、心理各模态的情感感知与认知计算，为研讨和传播情感计算领域最新学术和技术成果提供了最广泛的高层次交流平台。

在本届大会中，我们将举办“多领域多要素属性级情感分析”评测项目。属性级情感分析（Aspect-Based Sentiment Analysis, ABSA）是细粒度情感分析的一项重要任务，在学术界和工业界引起了广泛的关注。目前，尽管各种共享的ABSA任务和数据集已经被提出，但仍然缺少一个多领域多要素的大型ABSA数据集和一个覆盖多个领域的开放领域评估方式。尤其在文本情感分析任务面临ChatGPT等大模型冲击的背景下，上述评估显得更加重要。因此，我们标注了一个多领域多要素属性集情感分析数据集，覆盖属性、类别、观点、情感四种要素，支持隐式评价对象和隐式观点表达，包含五个典型领域。我们基于该数据，设定了Aspect-Sentiment二元组抽取、Aspect-Category-Opinion-Sentiment四元组抽取两个评测任务，每个任务又分别设置了特定领域和开放领域两种评估方式，后者允许使用包括ChatGPT在内的外部资源。

本届评测由中国中文信息学会情感计算专委会（CIPS-CCAC）主办，南京理工大学文本挖掘实验室（NUSTM）承办，诚挚欢迎各界人士参与。

## 评测内容

本届多领域多要素ABSA评测比赛包含2个子任务，任务内容覆盖Aspect-Sentiment二元组抽取和Aspect-Category-Opinion-Sentiment（ACOS）四元组抽取。本届比赛我们提供了一个多领域的英文数据集作为评测语料。

### 任务描述

#### 任务一：Aspect-Sentiment二元组抽取

给定一个评论句子，参赛模型需抽取出当前句子中所有的Aspect-Sentiment二元组（即一体化属性抽取与属性情感分类），输出的二元组只需包含显式属性。

#### 任务二：Aspect-Category-Opinion-Sentiment四元组抽取

给定一个评论句子，参赛模型须识别当前句子的所有Aspect-Category-Opinion-Sentiment (ACOS) 四元组[7]，输出的四元组包括显式和隐式的属性和观点。

#### 两个任务分别在特定领域和开放领域两种设定下评估：

在特定领域设定下，基于各自领域的训练数据建立领域特定的模型，并在各自领域的测试数据上进行预测。模型构建不允许使用外部标注数据，仅可使用开源的预训练语言模型。

在开放领域设定下，仅能建立一个模型，利用该模型在所有领域的测试数据上进行预测。允许使用所有领域的训练数据，也允许使用包括ChatGPT在内的外部资源。

### 数据集描述

我们从AirBnb、Yelp等公开网站上收集了五个领域（Book, Clothing, Hotel, Restaurant和 Laptop）的英文产品评论，由专业标注员进行了Aspect-Sentiment二元组和ACOS四元组的标注，整理为json格式的文件。

任务一的数据样例如下：
输入：I have read a lot of Stuart McBride books and loved them.
输出：(Stuart McBride books-Positive)

输入：The material feels nice but Amazon has up the wrong size chart!	
输出：(material-Positive), (size chart-Negative)

输入：This is a super fast computer and I really like it.
输出：(computer-Positive)

任务二的数据样例如下：

输入：Looks nice, and the surface is smooth, but certain apps take seconds to respond.
输出：(NULL-Display#Design_features-nice-Positive), (surface-Laptop#Design_features-smooth-Positive), (apps-Software#General-NULL-Negative）

输入：The food is great, migas are the best in the city!	
输出：(food-Food#Quality-great-Positive), (migas-Food#Quality-best-Positive)

输入：Highly recommended for a brief business trip or a leisure stay with your best friend.	
输出：(NULL-Hotel#General-Highly recommended-Positive)


###评估指标
F1 score
任务一：预测出的二元组被视为正确的当且仅当它与真实标签的属性和相应的极性完全匹配。
任务二：预测出的四元组被视为正确的当且仅当它的四种要素及其组合与真实四元组中的完全相同。

##报名网站

https://docs.qq.com/form/page/DU2NJa3BsZWRkSVl0

## 重要日期

时区：GMT+08:00

| 事项                 | 时间          |
| -------------------- | ------------- |
| 任务发布与报名启动   | 2023年4月10日 |
| 训练集语料发布       | 2023年5月01日  |
| 测试集语料发布       | 2023年6月12日  |
| 提交截止（报名结束） | 2023年6月15日 |
| 比赛结果公布         | 2022年6月22日 |

## 评委会成员

- 评测委员会成员：夏睿（南京理工大学）、虞剑飞（南京理工大学）、吴震（南京大学）、赵妍妍（哈尔滨工业大学）

## 联系方式

如有疑问，请致信评测会务组：蔡鸿杰hjcai@njust.edu.cn、宋楠 nsong@njust.edu.cn 

## 参考资料与文献

```
@inproceedings{DBLP:conf/acl/CaiXY20,
  author    = {Hongjie Cai and
               Rui Xia and
               Jianfei Yu},
  editor    = {Chengqing Zong and
               Fei Xia and
               Wenjie Li and
               Roberto Navigli},
  title     = {Aspect-Category-Opinion-Sentiment Quadruple Extraction with Implicit
               Aspects and Opinions},
  booktitle = {Proceedings of the 59th Annual Meeting of the Association for Computational
               Linguistics and the 11th International Joint Conference on Natural
               Language Processing, {ACL/IJCNLP} 2021, (Volume 1: Long Papers), Virtual
               Event, August 1-6, 2021},
  pages     = {340--350},
  publisher = {Association for Computational Linguistics},
  year      = {2021},
}
```

## 致谢

- 主办方：中国中文信息学会情感计算专委会（筹）（CIPS-CCAC）

- 承办方：南京理工大学文本挖掘实验室（NUSTM）、南京大学自然语言处理实验室（NJU-NLP）、哈尔滨工业大学赛尔实验室（HIT-SCIR）


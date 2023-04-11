# CCAC2023多领域多要素属性级情感分析评测

## 背景

“第三届中国情感计算大会”（Chinese Conference on Affect Computing, CCAC 2023）将于2023年7月在陕西西安召开。CCAC聚焦情感计算处理的前沿研究，为传播情感计算最新的学术和技术成果提供交流平台。中国情感计算大会每年举办一次，现已成为自然语言处理、社会计算领域的重要学术活动。第三届中国情感计算大会（CCAC 2023）由中国中文信息学会情感计算专委会（筹）主办，西安交通大学承办。作为中国中文信息学会（国内一级学会）在情感计算领域的重要会议，CCAC聚焦于语言、语音、视觉、生理、心理等多模态的情感感知与认知计算，为研讨和传播情感计算领域最新学术和技术成果提供了高层次交流平台。

在本届大会中，我们将举办“多领域多要素属性级情感分析”评测项目。属性级情感分析（Aspect-Based Sentiment Analysis, ABSA）是细粒度情感分析的一项重要任务，在学术界和工业界引起了广泛的关注。目前，尽管各种共享的ABSA任务和数据集已经被提出，但仍然缺少一个多领域多要素的大型ABSA数据集和一个覆盖多个领域的开放领域评估方式。尤其在文本情感分析任务面临ChatGPT等大模型冲击的背景下，上述评估显得更加重要。因此，我们标注了一个多领域多要素属性集情感分析数据集，覆盖属性、类别、观点、情感四种要素，支持隐式评价对象和隐式观点表达，包含五个典型领域。我们基于该数据，设定了Aspect-Sentiment二元组抽取、Aspect-Category-Opinion-Sentiment四元组抽取两个评测任务，每个任务又分别设置了特定领域和开放领域两种评估方式，后者允许使用包括ChatGPT在内的外部资源。

本届评测由中国中文信息学会情感计算专委会（CIPS-CCAC）主办，南京理工大学文本挖掘实验室（NUSTM）承办，诚挚欢迎各界人士参与。

## 评测内容

本届多领域多要素ABSA评测比赛包含2个子任务，任务内容覆盖Aspect-Sentiment二元组抽取和Aspect-Category-Opinion-Sentiment（ACOS）四元组抽取。本届比赛我们提供了一个多领域的英文数据集作为评测语料。

Aspect-Sentiment二元组抽取：1）Aspect表示表达了观点的实体或属性片段； 2）Sentiment表示针对实体或属性的情感极性。

Aspect-Category-Opinion-Sentiment四元组抽取： 1）Aspect表示表达了观点的实体或属性片段； 2）Category表示所关注实体或属性的预定义类别； 3）Opinion表示与实体或属性相关的情感表达片段； 4）Sentiment表示针对实体或属性的情感极性。特别地，隐式Aspect和隐式Opinion均用“NULL”来表示。

## 数据集

我们从Amazon、Yelp、AirBnb等公开网站上收集了五个领域（Book, Clothing, Hotel, Restaurant和 Laptop）的英文产品评论，由专业标注员进行了Aspect-Sentiment（AS）二元组和Aspect-Category-Opinion-Sentiment（ACOS）四元组的标注，整理为json格式的文件。标注规模如表1所示。

|      领域      | **标注句子** | **Aspect** | **Category** | **Opinion** | **Sentiment** | **AS二元组** |**ACOS四元组** |
| :------------: | :------------: | :--------------: | :------------: | :--------------: | :------------: | :--------------: | :--------------: |
|   **Books**    |      2967      |   3781    |   3593    |   4291   |   3781    |   3931    |   4507    |
|  **Clothing**  |      2373      |       2843      |   2994    |   3341   |   2843   |   2904    |   3416    |
|   **Hotel**    |      3526      |       4700      |   4886    |   5781  |   4700   |   4735|      6017    |
| **Restaurant New** |      5152      |       7056      |   6307    |   7958  |   7056   |   7250|   8496    |
|   **Laptop New**   |      4076      |      4958     |   4992    |   5378 |   4958   |   5035|   5758    |
|   **Total**   |      18094      |      23338     |   22772    |   26749 |   23338   |   23855|   28194    |

表1. 数据集规模统计

## 评测任务

### 任务一、Aspect-Sentiment二元组抽取

给定一个评论句子，参赛模型需抽取出当前句子中所有的Aspect-Sentiment二元组（即一体化属性抽取与属性情感分类），输出的二元组只需包含显式属性。

#### 示例：

```
Input: I have read a lot of Stuart McBride books and loved them.
Output: (Stuart McBride books-Positive)

Input: The material feels nice but Amazon has up the wrong size chart!	
Output: (material-Positive), (size chart-Negative)

Input: This is a super fast computer and I really like it.
Output: (computer-Positive)
```

#### 评价指标：

F1 score（预测出的二元组被视为正确的当且仅当它与真实标签的属性和相应的极性完全匹配）。

该任务分别在特定领域和开放领域两种设定下评估：
- 特定领域设定：基于各自领域的训练数据建立领域特定的模型，并在各自领域的测试数据上进行预测。模型构建不允许使用外部标注数据，仅可使用开源的预训练语言模型。
- 开放领域设定：仅能建立一个模型，利用该模型在所有领域的测试数据上进行预测。允许使用所有领域的训练数据，也允许使用包括ChatGPT在内的外部资源。


### 任务二、Aspect-Category-Opinion-Sentiment四元组抽取

给定一个评论句子，参赛模型须识别当前句子的所有Aspect-Category-Opinion-Sentiment (ACOS) 四元组[7]，输出的四元组包括显式和隐式的属性和观点。

#### 示例：

```
Input: Looks nice, and the surface is smooth, but certain apps take seconds to respond.
Output: (NULL-Display#Design_features-nice-Positive), (surface-Laptop#Design_features-smooth-Positive), (apps-Software#General-NULL-Negative）

Input: The food is great, migas are the best in the city!	
Output: (food-Food#Quality-great-Positive), (migas-Food#Quality-best-Positive)

Input: Highly recommended for a brief business trip or a leisure stay with your best friend.	
Output: (NULL-Hotel#General-Highly_recommended-Positive)
```

#### 评价指标：

F1 score（预测出的四元组被视为正确的当且仅当它的四种要素及其组合与真实四元组中的完全相同）。

该任务分别在特定领域和开放领域两种设定下评估：
- 特定领域设定：基于各自领域的训练数据建立领域特定的模型，并在各自领域的测试数据上进行预测。模型构建不允许使用外部标注数据，仅可使用开源的预训练语言模型。
- 开放领域设定：仅能建立一个模型，利用该模型在所有领域的测试数据上进行预测。允许使用所有领域的训练数据，也允许使用包括ChatGPT在内的外部资源。

## 报名网站

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

## 参考文献

[1]	Bing Liu. Sentiment analysis and opinion mining. Synthesis lectures on human language technologies, 2012.

[2]	Hongjie Cai, Yaofeng Tu, Xiangsheng Zhou, Jianfei Yu, and Rui Xia. Aspect-category based sentiment analysis with hierarchical graph convolutional network. COLING 2020.

[3]	Margaret Mitchell, Jacqui Aguilar, Theresa Wilson, Benjamin Van Durme. Open Domain Targeted Sentiment. EMNLP 2013.

[4]	Minghao Hu, Yuxing Peng, Zhen Huang, Dongsheng Li and Yiwei Lv. Open-Domain Targeted Sentiment Analysis via Span-Based Extraction and Classification. ACL 2019.

[5]	Jeremy Barnes, Robin Kurtz, Stephan Oepen, Lilja Øvrelid, Erik Velldal. Structured Sentiment Analysis as Dependency Graph Parsing. ACL 2021.

[6]	Yifei Yang, Hai Zhao. Aspect-based Sentiment Analysis as Machine Reading Comprehension. COLING 2022.

[7]	Hongjie Cai, Rui Xia, and Jianfei Yu. Aspect-category-opinion-sentiment quadruple extraction with implicit aspects and opinions. ACL 2021.

[8]	Evgeny Kim and Roman Klinger. Who feels what and why? annotation of a literature corpus with semantic roles of emotions. COLING 2018.

[9]	Xin Li, Lidong Bing, Piji Li, and Wai Lam. A unified model for opinion target extraction and target sentiment prediction. AAAI 2019.

[10]	 Maria Pontiki, Dimitrios Galanis, Haris Papageorgiou, Ion Androutsopoulos, Suresh Manandhar, Mohammad Al-Smadi, Mahmoud Al-Ayyoub, Yanyan Zhao, Bing Qin, Orphée De Clercq, et al. Semeval2016 task 5: Aspect based sentiment analysis. In 10th International Workshop on Semantic Evaluation (SemEval 2016).

[11]	 Maria Pontiki, Dimitrios Galanis, Harris Papageorgiou, Suresh Manandhar, and Ion Androutsopoulos. Semeval-2015 task 12: Aspect based sentiment analysis. In Proceedings of the 9th international workshop on semantic evaluation (SemEval 2015).

[12]	 Maria Pontiki, Dimitris Galanis, John Pavlopoulos, Harris Papageorgiou, Ion Androutsopoulos, and Suresh Manandhar. SemEval-2014 task 4: Aspect based sentiment analysis. In Proceedings of the 8th International Workshop on Semantic Evaluation (SemEval 2014).

[13]	 Wenxuan Zhang, Yang Deng, Xin Li, Yifei Yuan, Lidong Bing, and Wai Lam. Aspect sentiment quad prediction as paraphrase generation. EMNLP 2021.

[14]	 Xiaoyi Bao, Wang Zhongqing, Xiaotong Jiang, Rong Xiao, Shoushan Li. Aspect-based Sentiment Analysis with Opinion Tree Generation. IJCAI 2022.

## 致谢

- 主办方：中国中文信息学会情感计算专委会（CIPS-CCAC）

- 承办方：南京理工大学文本挖掘实验室（NUSTM）、南京大学自然语言处理实验室（NJU-NLP）、哈尔滨工业大学赛尔实验室（HIT-SCIR）


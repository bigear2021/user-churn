# user-churn
基于用户行为序列的流失率预测

* <font size=4>背景</font>：
<br/>深度学习不仅在NLP和CV领域取得了重要突破，在推荐与广告系统等经典互联网应用中也有很多应用。长期以来用户行为序列分析与预测都是推荐/搜索/广告等领域的重要课题。本文基于前人针对社交网络用户流失的分析方法，分析了音乐APP用户的行为习惯，建立了lightGBM和LSTM预测模型。
  
  
* <font size=4>结论</font>：
* 1.基于用户活跃天数的LSTM模型能有效预测用户的流失情况，效果(F1得分0.98)略低于经典的模型lightGBM(F1得分0.99)。
* 2.词向量与tsne结合的方式，能够有效的提取歌曲风格和用户关注话题信息。
* 3.用户流失(留存)最关键的因素是：最后1次使用日期，使用天数，平均每(活跃)天收听的歌曲数，是否vip客户，平均每(活跃)天操作次数，用具体的操作类型、操作页面、用户基础属性等因素关系不大。
  
  
* <font size=4>方法</font>:
* 1.用户行为序编码。
* 2.基于bert-embedding+tsne的词向量编码。
* 3.Kmeans聚类。
* 4.lightGBM分类与SHAP解释。
* 5.LSTM序列预测。
  
  
* <font size=4>主要参考文献</font>：
<br/>[I Know You’ll Be Back: Interpretable New User Clustering and Churn Prediction on a Mobile Social Application](https://arxiv.org/abs/1910.01447)
<br/>由于作者没有提供数据集，只能根据作者提供的[源码](https://github.com/yangji9181/ClusChurn)，使用[2021DIGIX赛题数据集](https://developer.huawei.com/consumer/cn/activity/devStarAI/algo/competition.html#/preliminary/info/004/data)近似复现。
比赛数据（采样+脱敏后）抽取的时间范围是连续60 天的用户行为数据和行为对应匹配的用户、歌曲、歌手数据。
  
  
* <font size=4>其他参考文献</font>：
* 基于lstm和cnn的方法:[ChurnPrediction](https://github.com/SingingData/ChurnPrediction),[《自然语言处理：基于预训练模型的方法》4.6.7基于循环神经网络的情感分类](https://github.com/HIT-SCIR/plm-nlp-code/blob/main/chp4/lstm_sent_polarity.py)
* 基于lightGBM的方法:[客户流失预测及营销方案](https://mp.weixin.qq.com/s/nq_ZX6u8o5S_phrJ3AFOvg)，[源码](https://github.com/aialgorithm/Blog/tree/master/projects/%E5%AE%A2%E6%88%B7%E6%B5%81%E5%A4%B1%E9%A2%84%E6%B5%8B%E5%8F%8A%E8%90%A5%E9%94%80),[可解释机器学习-shap value的使用](https://blog.csdn.net/qq_41103204/article/details/104896630)
* [推荐中的序列化建模：Session-based neural recommendation](https://zhuanlan.zhihu.com/p/30720579)
* [DeepCTR：易用可扩展的深度学习点击率预测算法包](https://zhuanlan.zhihu.com/p/53231955)
  
  
* <font size=4>思考</font>：
* 1.数据格式的整理占用了80%的时间，实际工作接触的数据往往会比竞赛数据有更多的异常。
* 2.由于作者未能提供原始数据，很多情况下只能猜测源码的思路，比较吃力，说明一个好的分享应该尽可能完整，方便复现。
* 3.深度学习的难度一方面在于模型本身(包括数学原理)的复杂，另一方面在于NLP/CV之外的案例很少，需要大量查阅+尝试才能形成匹配的思路。
* 4.硬件资源(特别是GPU)限制了很多从建模到调参的很多想法。
* 5.现实中大量的不均衡类别场景，如果能根据业务设计优化目标(损失函数)，也许会比经典的F1、混淆矩阵评估更有价值。

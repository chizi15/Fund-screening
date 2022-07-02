# Fund-screening
Via TIanTian Fund, TongHuaShun iFund, and Alipay, to collect funds data, and through feature engineering to sort funds, and to form weights of chosen dunds

由于公募基金有超过1万支，一个一个筛选太费时费力，本方法就以支付宝、天天基金、同花顺爱基金、国元证券、平安爱基金等基金销售平台推荐的基金为基础，对这些基金的评分数据进行统计、数值变换、排序筛选，可以得到当前各个基金的持仓权重。并可等待每季度基金公布持仓数据后，重新做一遍上述流程：即更新推荐基金、对基金评分数据进行重新统计、数值变换、排序筛选、计算权重，此时新权重和现有持仓权重一定或多或少地存在偏差，则可进行买卖操作将持仓调整为当前新一期的权重。类似于股票指数的调整流程，定期对构建的个性化基金指数进行调整。

后期会定期持续更新，本人也按照该流程操作，避免个人纪律性的缺乏，对数据全面性掌握的欠缺，以及花费过多时间在基金选择、时机选择、买卖量选择等方面或者犹豫难以抉择。

在该表的字段中，Normalizer是对原始数据做标准化，因为每一个字段的原始数据的分布特征有所不同，直接平均是“不公平”的，那些分布得更离散的字段，对于每一行的数据，也即每一个基金的数据，会天然占有更大的相对权重，即它们对总分的影响更大。除以各自标准差后，会大大减小这种不良影响。

再对每一个“××综合”字段做MinMaxScale，可进一步减小上述分布特征不同带来的不良后果，并将得分转化为分位数，对它们进行简单算术平均后即可得到总分。因为每一个“××综合”字段不会存在离群值，所以用MinMaxScale即可，无需使用robust scaling等方法。

Difference是总分的一阶差分序列，根据个人对持仓数量的偏好，通常在排名30~40的基金中找一个Difference最大的或较大的基金，作为临界基金即可。不可太少，也无需过多，参照中心极限定理的思想。对以上的基金进行（自动止盈）定投，或者每个季度按该方法重新排序计算权重，以此结果进行调仓。

经理及属性记录该基金的经理，因为基金主要看经理，如果被筛选出的基金有相同的经理，则可视情况是否去重，以保证构建出的基金指数都来源于不同的经理，即不同的认知。

买入可按权重分批次逐步操作，卖出可按比例分批次逐步操作，以增加收益或较少亏损的概率。

除原始数据字段的中间字段的计算公式也在表中。

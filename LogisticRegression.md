1.逻辑回归原理
逻辑回归(LogisticRegression)是机器学习中最简单的分类模型。
训练集中的样本只有两类，我们用{0,1}表示，即预测结果是离散的,只取0或1。
这时我们可以认为一个样本属于1的机率是其本身的属性线性加权得到的。
当该数值大于0时，样本类别(y)为1；
当该数值小于0时，样本类别为0；
逻辑回归最理想的模型是单位阶跃函数，但该函数不连续，无法求导，实际使用中无法训练。
因此，我们用sigmoid函数作为模型，通过梯度下降等方式可训练出模型参数。

2.正则化
相对于线性模型，逻辑回归的模型复杂度要高一些。逻辑回归的正则化有L1正则化和L2正则化。
L1正则化，会使得对结果影响较小的特征权重为0，这是一个很好的特性，可以过滤掉一些特征。
L2正则化，会尽可能多的保留所有特征，对结果影响较小的特征权重会较小，但不会取到0。

3.数据不均衡问题处理办法
数据不均衡问题在实际工程中也是很常见的。比如：CTR预估、欺诈用户识别、保险赔付率预估。
之前做过一个保险赔付率预估的项目，在所有投保人群中，仅有不到10%的用户会出险并申请赔偿。
大额赔付用户比例更低，0.1%左右。如果不对样本进行处理，几乎所有的模型决策树、FR、xgboost、svm、lr。
准确率奇高，90%多。但这些模型没有任何价值，因为他们几乎把所有用户都判断为不会出险。
这也引出了模型评价指标，模型的准确率并不是唯一指标，很多情况下，我们评价模型的好坏或者说模型效果的好坏。
要从多方面评估：如对正负样本的召回、在同一预测分类中正负样本的混杂度等。

对于此类问题，我倾向于使用欠采样。使得征服样本比例接近1:1再进行训练。
对于多分类问题，如果样本量不足，在业务允许的情况下可考虑修改分类边界或者合并部分子类的方式学习。
如果样本实在太少，建议通过差值方式，扩大训练集范围， 然后在进行欠采样。
直接人工增加负样本个数方法，我个人持保留态度。

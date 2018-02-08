##概要
从生物学角度看 ， 修正神经元比sigmoid神经元更切合实际情况， sigmoid又优于tanh, 但是多层神经网络中tanh神经元效果优于sigmoid。 修正神经元尽管在0点非线性且不可微但在实际效果中要优于tanh神经元。 且re可以产生稀疏表示

##介绍
在ml研究人员、计算神经学家的nn模型之间存在很多不同。主要是因为二者的目标不一样： 前者旨在找到可计算的、有效的、容易泛化到新样本的learner, 后者旨在提取神经科学数据的同时获取数据本质的解释， 为未来的生物实验提供预言和指导。因此两者共同关注的目标就值得研究。 本文通过rectifier activation function来打通两者的隔阂。 近期统计学习领域的理论和经验工作证明算法在深度架构的重要性。 这主要受由链式处理单元组成的哺乳动物视觉皮层启发，处理单元之间通过对原始输入信息的不同表征来关联起来。 这在灵长类动物的视觉系统中特别的清晰， 视觉的处理分为不同的stage: 探测边，形状，逐步到更复杂的视觉形状。 更深层学到的特征会组合前面层的特征， 且随着层次的加深，浅层特征不再变化
在2006年提出的dbn可以认为是深度网络的训练一个突破，更通俗的讲：通过非监督学习来初始化每层网络。一些曾试图理解非监督学习过程是怎样启到作用的，同时另外一些在研究原始的训练方式为什么会失败。
我们来探究使用rectified non-linearity 来替代sigmoid or tanh. 对于无界激活函数会使用l1 正则项来实现稀疏性和避免数字下溢。 hinton等人已经在RBM中展现了这种激活函数的光明前景（相对于logistic sigmoid激活函数）。 我们的工作继承于此，针对使用pre-training的denoising auto-encoders。 在图片分类基准上对relu和tanh提供了广泛的经验对比, 同时包含文本的语义分析领域。

我们的实验表明当人工神经元未激活或者以线性方式运行的时候，预训练能产生更好的效果。令人吃惊的是， rectifying激活函数在不进行非监督预训练的时候也很取得最好效果。 rectifier 网络仍能从非监督预训练中受益： 当有大量未标注样本时，可以使用半监督学习方式。 此外， rectifier 单元可以天然的产生稀疏网络，与生物神经元的工作方式相近， 这也架起了机器学习与神经科学关于激活函数和稀疏性方面的桥梁。

关于大脑能量消费的研究表明： 神经元用稀疏、分布式的方式来编码信息。 同时能够处理激活状态的神经元只占到1%--4%。 这是丰富表示和最小动作能量消耗之前权衡的结果。 如果不使用正则项， 一般的前馈网络不具有这些特征。 例如，sigmoid激活函数在0.5附近有稳定的状态， 初始化权重较小时，所有的神经元在达到一半的饱和度时开始fire. 这在生物学上难以置信并且不利于基于梯度的优化。
生物学和机器学习模型的重大差异在于非线性激活函数。
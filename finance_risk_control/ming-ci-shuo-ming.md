# 名称说明

### 现金贷
是小额现金贷款业务的简称，是针对申请人发放的消费类贷款业务，具有方便灵活的借款与还款方式，以及实时审批、快速到账的特性。 直接出借资金而不考虑消费场景

### 消费金融
消费金融公司是指经中国银行业监督管理委员会批准，在中华人民共和国境内设立的，不吸收公众存款，以小额、分散为原则，为中国境内居民个人提供以消费为目的的贷款的非银行金融机构。有消费场景的出借

### P2P
P2P是英文peer to peer lending（或peer-to-peer）的缩写，意即个人对个人（伙伴对伙伴）。又称点对点网络借款，是一种将小额资金聚集起来借贷给有资金需求人群的一种民间小额借贷模式。属于互联网金融（ITFIN）产品的一种。属于民间小额借贷，借助互联网、移动互联网技术的网络信贷平台及相关理财行为、金融服务。

### 现金贷名词
    逾期：一般所说的逾期是指超过规定的最后还款期限，未及时足额将所消费款项存入指定账户的情形

    首逾：用户在一家平台上的首次逾期
    
    口子：是小额贷APP，通俗的讲就是用手机借钱的软件。
    
    撸贷：恶意借钱，不打算还的人
    
    风控：通过一定的审核策略，比如芝麻分等等对借款人进行审核，降低坏账的一种行为。
    
    催收：对欠款进行补救的民事行为。比如电话提醒，电话跟进等等。
    
    进件：你提交的申请贷款订单
    
    均件：每个人申请叫进件，通过叫过件，过件的平均金额叫均件
    
    申请：提交的申请贷款订单
    
    复借：获取从开始时间至结束时间内，有过申请借款行为，且成功借款次数大于等于n次的用户数。
    
    提额：对借款额度进行提升
    
    前期：要贷款必须收取一定的费用，不然不给贷款
    
    联登：联合登陆，部分贷超规定，现金贷要合作的话，必须进行联合登陆
    
    库存：上线以来的累计注册用户。
    
### vintage
我们在比较放贷质量的时候，也要按账龄（month of book，MOB  ）的长短同步对比，从而了解同一产品不同时期放款的资产质量情况。
举例来说，今天是2018年5月25日，我们取今天贷款第一期到期的客户作为观察群体，观察他们今后29天的还款情况。如果你将将今天所有贷款到期的客户作为观察群体（里面有第一期到期的，也有第二期到期的，也有第三期到期的，等等），那么这个群体里面的客户就不是位于同一层面上了。
以上就是vintage的介绍。传统的销售统计报表大多数情况下只是将不同渠道、不同时间、不同产品的数据进行统计，是顺序的，平面的。vintage将不同时期的数据拉平到同一时期比较，可以很直观地比较和反思不同时期公司的营销策略的效果。

### 迁移率
  在说迁移率之前，我们先定义逾期阶段的概念。逾期就是说你到了该还款的日子而没有还款，那你就进入了逾期。根据逾期天数，又分为M0-M7+等八个阶段。没有逾期的是M0，逾期1~29天的是为M1，逾期30~59的定义为M2，以此类推，逾期超过180天的定义为M7+。
  
  有了逾期阶段的概念，迁移率就好理解了。简单说，就是处于某一逾期阶段的客户转到其他逾期阶段的变化情况。迁移率通常可以用来预测不同逾期阶段的未来坏账损失。比如，M2-M3，说的是从逾期阶段M2转到逾期阶段M3的比例。需要注意的是，我们应该选还款日为同一天的M2来做分子，如下。
  迁移率是催收常使用的绩效指标。它与vintage结合能实现风险的精细化管理。vintage的核心思想是对不同时期的同一层面的资产进行分别跟踪，按照账龄长短进行同步对比，从而了解不同时期的资产质量情况，是一个所谓竖切的概念；而迁移率能很好的提示客户整个生命周期中的衍变情况，是一个所谓横切的概念。
  
###滚动率

在风险控制中，我们的根本目的是识别坏用户，通过历史数据，抓取坏客户显著区别于正常客户的特征，并以此为标准去预测未来的坏客户。用户的好坏其实很难定义，不能说逾过期的用户就是坏用户，也许人家其实想还，只是不小心忘记还款了呢。而且，有的时候，“适当”的逾期还能增加公司的逾期利息收入。我们所关注的坏客户是坏到某一程度，也就是逾期等级较高且不还款的客户。

  前面说的vintage是从时间维度上判断客户群体的好坏，下面说的滚动率则是从行为程度上判断客户的好坏，它可以帮助我们判断某些逾期客户是否还可以再抢救一下，收回点成本。

    滚动率，简单地说就是以某一时间点为观察节点，观察客户在该点前一段时间内（比如半年）最坏逾期阶段，并追踪其在观察点之后的一段时间向其他逾期阶段发展的情况，特别是向更坏程度发展的情况。举个栗子，今天是2018年5月25日，取今天的1万个客户，统计他们在过去半年里的最大逾期阶段。然后追踪他们后半年的表现。以下数字纯属虚构，完全是为了说明问题，各个公司有自己的观察数据和追踪数据。

    M0的客户在未来半年里，98%的客户还是会保持正常M0的状态

    最大逾期阶段M1的客户在未来80%会变M0，但是还有20%会继续，甚至有5%的人往更坏的程度发展

    最大逾期阶段M2的客户在未来40%的人会继续恶化，22%左右的人会变M0（完全从良）；

    最大逾期阶段M3的客户在未来60%的人会继续恶化，15%左右的人会变M0（完全从良）；

    最大逾期阶段M3+的客户在未来80%的客户会继续此状态（没救了）。

### 入催率

有了前面的铺垫，入催率就比较简单了。它指的是在某一个还款日，客户从M0变成M1的比例。比如说，今天，有N个M0客户到了还款日，里面有M个客户按时还款了，那么今天的入催率就是（N-M）/N。它与下面的FBD是有区别的。
    
### FPD
是指首期逾期率，是说在某一个还款日，仅第一期到期的客户中有多少没有按时还款。与入催率的差别在于，入催率包含了第一期、第二期、第三期等等所有到期的M0。FPD一般用来做反欺诈，因为欺诈用户他第一期是根本不会还款的。 

### IRR 与 APR
APR：Annual Percentage Rate。 当计算周期小于一年的时候，存在复利， 收益会多一点。 计算公式：n为计息周期。 (1+利率/n）^n 年度百分率。 
IRR： 内部收益率， 一般按天计算， 不进行复利计算。利息较apr低。




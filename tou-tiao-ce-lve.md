### 背景
- 

### 策略链
#### pre_node
- baseline: age < 18 or job=student
- 取ToutiaoCa: PRSCASnapshot

#### FeatureCalculate1
- 特征算子配置文件： TouTiaoCa  
    - ApplicationInfoFeature
    - DeviceCallsFeature
    - SpFeature
    - DeviceSmsFeature
    - TongdunFeature
    - GraphPara1Feature
    - AppListFeature
    - JingdongFeature
    - GraphPara2Feature
    - TaobaoFeature
    - CombineComunicationFeature
    - ShumeiOverdueFeature
    - DeviceContactFeature
    - DeviceFeature
    - GraphFeature
    - CommunicationConvergedFeature
    - MoxieSocialInsuranceFeature
    - AuthInfoFeature
    - ContactFeature
    - TaobaoUpcFeature
    - Tongdun2lFeature
    - UserInfoFeature
    - ServiceProviderFeature
    - UpcFeature
    - JoinParameterFeature
    - UserActionFeature
    - BaiduRiskFeature
    - MoxieAccumulationFundFeature
    - BaiqishiFeature
    - ApplicationHistoryFeature
    - JingdongUpcFeature
    - MoxieCreditCardMailFeature
    - ZzcFeature
    - SmsFeature
    - ShumeiMultiloanFeature
    - ThirdCoreParameterFeature
    
    
- 特征选择文件： yqb_basic
- 特征获取失败后重试： sp\_error,  feature\_1_error
- amount_feature置0: fmap['1019991000'] = 0

#### anti-cheat
- anti_cheat_conf:
   - ug_model, 使用4个特征， 老用钱宝/大额的订单申请/放款总次数
   - rule_model, 没有特征
   - outlier_model, 特征较多，短信\applist等其它特征
   - scorecard_model， 没有特征
- 获取各个模型分并标记反欺诈结果，但不决策。
- next-node: Personas

#### Personas
- 根据order_id, user_id, identity以及fmap, 获取Personas的结果： loan_history_level

#### ModelScore
- 获取recall_score_old/new
- 不出错即进入下一节点

#### baselinse1
- 根据订单类型进行baseline验证
    - regular: 1021401002 > 0 用户在大额历史放款订单数
    - member: 1021701001 > 0
    - recall: 1021001004 > 0 , 用户在-老用钱宝-历史订单-用钱宝历史放款总次数
    - first: 1022001002 = 0 (用钱宝授信拒绝次数==0) and 1021001007 == 0 (老用钱宝拒绝总次数==0) and 1022801002 == 0 (member?)
    - 其它是again
- first_baseline1:
    - check_job
    - check_age
    - check_anticheat
    - check_couple_on_loan
    - check_tongdun_black
    - check_court_blacklist_by_baidu
    - check_yqb_overdue
    - check_fqz_overdue
    - check_shumei_overdue_blacklist
    - check_white_knight_multiloan
    - check_tongdun_multiloan
    - check_xinyan_apply
    
- 只要不发生错误就流向下一节点

#### decision1 结束node
- 订单类型同baseline
- first授信阶段
    - 仅使用京东zrobot和冰鉴分决策
    - zrobot_score > 670 or binjian_score > 670 and review['baseline_suggestion'] == 1: 5000额度
    - zrobot_score > 670 and binjian_score > 670 and review['baseline_suggestion'] == 1: 8000额度
    
#### 当前头条和美图没有face_task节点， 需要开发
    
 

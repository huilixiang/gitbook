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
 

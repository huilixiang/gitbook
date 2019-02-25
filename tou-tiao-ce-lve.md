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
 

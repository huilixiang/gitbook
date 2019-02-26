### 背景

### 策略链
#### Pre_DN
- age > 18
- job != '学生'
- YQBCASnapshot, product=800

#### FeatureCalculate1
- MeituCa 
 

- yqb_basic  

    "ApplicationInfoFeature",
    "DeviceCallsFeature",
    "SpFeature",
    "DeviceSmsFeature",
    "TongdunFeature",
    "GraphPara1Feature",
    "AppListFeature",
    "GraphPara2Feature",
    "CombineComunicationFeature",
    "ShumeiOverdueFeature",
    "DeviceContactFeature",
    "DeviceFeature",
    "GraphFeature",
    "CommunicationConvergedFeature",
    "AuthInfoFeature",
    "ContactFeature",
    "Tongdun2lFeature",
    "UserInfoFeature",
    "ServiceProviderFeature",
    "UpcFeature",
    "JoinParameterFeature",
    "BaiduRiskFeature",
    "BaiqishiFeature",
    "ApplicationHistoryFeature",
    "ZzcFeature",
    "SmsFeature",
    "ShumeiMultiloanFeature",
    "ThirdCoreParameterFeature",
    "XinyanApplyFeature",
    "XinyanBehaviorFeature",
    "BingjianFeature",
    "ZrobotFeature"
    
#### AntiCheat
- 获取anticheat的结果，但不决策  

#### ModelScore
- yqb_first_normal_mt， 可用特征列表 feature_conf/yqb36_first_mt.conf.json

- yqb36_meitu_maat_main_v2, 可用特征列表feature_conf/yqb36_meitu_maat_main_v2.0.conf.json

#### Baseline1_DN
- order_type: 
    - 1021011004 > 0 美图-历史订单-历史放款总次数
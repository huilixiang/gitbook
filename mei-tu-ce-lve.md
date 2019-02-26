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
    - 1021011004 > 0 美图-历史订单-历史放款总次数 regular
    - 1021031002 == 0 美图-授信历史-授信拒绝次数 and 1022001002 == 0 #用钱宝36-授信历史-授信拒绝次数 and 1021011007 == 0 美图-历史订单-历史拒绝总次数   
- check_job
- check_age_range
- check_is_not_phone
- check_sp_name_ok
- check_call_times_six_month
- check_multi_idcard
- check_anticheat 
- check_couple_on_loan
- check_tongdun_black
- check_court_blacklist_by_baidu
- check_yqb_overdue
- check_fqz_overdue
- check_shumei_overdue_blacklist
- check_white_knight_multiloan
- check_tongdun_multiloan

#### Decision1_DN
- user_type/first 
    - 授信1
    - yqb_first_normal_mt_dai_score > 820 or yqb36_meitu_maat_main_v2.0_dai_score > 650
    - 在授信2检查baseline
    
    - 订单1
    - model_suggestion && baseline_suggestion , 3000  

#### FeatureCalculate2_DN
- MeituCa 
- yqb_cheap

#### baseline2
- check_xinyan_apply  loan_overdue_num_thresh=0

#### 
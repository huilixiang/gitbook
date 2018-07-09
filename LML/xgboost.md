### xgboost学习
#### 核心流程
- cli_main.cc  
    - CLITrain
    - CLIPredict
    
- CLITrain
    - learner-> configure (learner.cc)
    - learner-> initmodel
    - learner-> updateoneiter 

- learner.cc -> updateoneiter 
    - learner.PredictRaw
    - obj_->GetGradient (ObjFunction, learner.h)
    - gbm_->DoBoost (GradientBooster, learner.h)

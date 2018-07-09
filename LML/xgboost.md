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
    
- learner.predictraw
    - gbm_->PredictBatch
    
- gbm.PredictBatch
    - predictor->PredictBatch (cpu_predictor.cc or gpu_predictor.cc)

- cpu_predictor.PredictBatch 
    - PredLoopSpecalize
        - PredValue ## 一个样本的预估值等于每棵树所有叶子节点值的和 leaf_value是关键
            - int tid = trees[i]->GetLeafIndex(*p_feats, root_index);
            - psum += (*trees[i])[tid].leaf_value()


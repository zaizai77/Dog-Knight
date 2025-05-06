# Dog-Knight
一款RPG游戏项目文件


flowchart LR
  %% 注册／注销
  subgraph 注册／注销
    A[对象启用（OnEnable/Start）] -->|RegisterSaveData()| B[加入 saveableList]
    C[对象禁用（OnDisable）] -->|UnRegisterSaveData()| D[移除 saveableList]
  end

  %% 保存流程
  subgraph 保存流程
    E[广播 saveDataEvent] --> F[DataManager.Save()]
    F --> G{遍历 saveableList}
    G --> H[调用 GetSaveData(Data)]
    H --> I[写入 Data 实例]
  end

  %% 加载流程
  subgraph 加载流程
    J[广播 loadDataEvent] --> K[DataManager.Load()]
    K --> L{遍历 saveableList}
    L --> M[调用 LoadData(Data)]
    M --> N[应用到对象状态]
  end

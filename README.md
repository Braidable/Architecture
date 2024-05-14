# Architecture

## Model
### Training/Updates
```mermaid
   %%----- Generic Styling Classes -----%%
   %% Deep Azure Blue
   classDef Azure fill:#005A9E,stroke:#333,stroke-width:2px;
   %% Jungle Green
   classDef MachineLearning fill:#16A085,stroke:#333,stroke-width:4px;
   %% Dark Orange
   classDef ExternalData fill:#D35400,stroke:#333,stroke-width:2px;
   %% Dark Teal
   classDef ProcessFlow fill:#00796B,stroke:#333,stroke-width:2px;
   %% Dark Purple
   classDef Integration fill:#8E44AD,stroke:#333,stroke-width:2px;
   %% Dark Red
   classDef Security fill:#B03A2E,stroke:#333,stroke-width:2px;
   %%----- Generic Styling Classes -----%%

graph TD
  AzureMachineLearning(Azure Machine Learning) -->|Manages| ModelTraining(Model Training & Deployment)
  ModelTraining --> MLPipelines(ML Pipelines)
  MLPipelines -->|Updates Models| LLM(Generic LLM)
  %%AzureMachineLearning -.->|Automated ML & MLOps| AKS["Azure Kubernetes Service (AKS)"]
  AKS["Azure Kubernetes Service (AKS)"] --> |Hosts| LLM
  MLPipelines -->|Triggers| AzureFunctions[Azure Functions]
  AzureFunctions -->|Triggers Data Update| DataSyncWorkflows[Azure Logic Apps]


  class AzureMachineLearning,AKS,AzureFunctions,DataSyncWorkflows Azure;
  class ModelTraining,MLPipelines,LLM MachineLearning;
  class ExternalDataSources,Storage ExternalData;
```

### Data Updates
```mermaid
   %%----- Generic Styling Classes -----%%
   %% Deep Azure Blue
   classDef Azure fill:#005A9E,stroke:#333,stroke-width:2px;
   %% Jungle Green
   classDef MachineLearning fill:#16A085,stroke:#333,stroke-width:4px;
   %% Dark Orange
   classDef ExternalData fill:#D35400,stroke:#333,stroke-width:2px;
   %% Dark Teal
   classDef ProcessFlow fill:#00796B,stroke:#333,stroke-width:2px;
   %% Dark Purple
   classDef Integration fill:#8E44AD,stroke:#333,stroke-width:2px;
   %% Dark Red
   classDef Security fill:#B03A2E,stroke:#333,stroke-width:2px;
   %%----- Generic Styling Classes -----%%

graph TD
  AzureMachineLearning(Azure Machine Learning) -->|Manages| ModelTraining(Model Training & Deployment)
  ModelTraining --> MLPipelines(ML Pipelines)
  MLPipelines -->|Updates Models| LLM(Generic LLM)
  %%AzureMachineLearning -.->|Automated ML & MLOps| AKS["Azure Kubernetes Service (AKS)"]
  AKS["Azure Kubernetes Service (AKS)"] --> |Hosts| LLM
  MLPipelines -->|Triggers| AzureFunctions[Azure Functions]
  AzureFunctions -->|Triggers Data Update| DataSyncWorkflows[Azure Logic Apps]


  class AzureMachineLearning,AKS,AzureFunctions,DataSyncWorkflows Azure;
  class ModelTraining,MLPipelines,LLM MachineLearning;
  class ExternalDataSources,Storage ExternalData;
```

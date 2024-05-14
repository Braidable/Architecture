# Architecture

## Model
### Training/Updates
```mermaid
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
```

### Data Updates
```mermaid
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
```

### Data Retrieval
```mermaid
graph TD
  GenericLLM["Generic LLM"] -->|Interprets Context| ContextInterpreter["Context Interpreter"]
  ContextInterpreter -->|Determines Data Source| DecisionPoint{ }
  DecisionPoint -->|SQL Data Source| SQLGenerator["SQL Query Generator<br>(LLM)"]
  DecisionPoint -->|Cosmos DB Data Source| PeriodicallyUpdatedDatastores["Azure Cosmos DB & Azure Blob Storage"]
  SQLGenerator -->|Generates| ExternalDatabaseIntegration["External Database Integration"]
  ExternalDatabaseIntegration -->|Live Queries| CustomerDatabases["Customer Databases"]
  SchemaRegistry["Schema Registry"] -->|Informs| SQLGenerator


  class GenericLLM,SQLGenerator,ContextInterpreter MachineLearning;
  class SchemaRegistry Azure;
  class ExternalDatabaseIntegration Integration;
  class CustomerDatabases,PeriodicallyUpdatedDatastores ExternalData;

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
```

### Feedback Loops
```mermaid
graph TD
   %% Core Components
   AnonymizationService["Anonymization Service<br>(Azure Databricks/Azure Functions)"] --> AnonymizedData["Anonymized User Queries<br>(Azure Cosmos DB)"]
   RawUserQueries["Raw User Queries<br>(Azure Functions)"] --> AnonymizationService
   AnonymizedData --> RAG["Retrieval-Augmented Generation"]
   RAG --> LLM["Generic LLM<br>(Azure Kubernetes Service)"]
  
   %% User Interaction and Feedback
   UserFeedback["User Feedback<br>(Azure Functions)"] --> FeedbackAnalysis["Feedback Analysis<br>(Azure Machine Learning)"]
   FeedbackAnalysis --> ModelTraining["Model Training & Fine-Tuning<br>(Azure Machine Learning)"]
  
   %% Performance and Optimization
   UsageMetrics["Usage Metrics<br>(Application Insights)"] --> PerformanceOptimization["Performance Optimization<br>(Azure Monitor)"]
   DataSourceUsage["Data Source Usage<br>(Azure Logic Apps)"] --> DataIntegrationOptimization["Data Integration Optimization<br>(Azure Cosmos DB)"]
   PerformanceOptimization --> Infrastructure["Infrastructure Scaling<br>(Azure Kubernetes Service)"]
   DataIntegrationOptimization --> RAG
  
   %% Expanded Use of Anonymized Data
   AnonymizedData --> ModelTraining
   AnonymizedData --> UserBehaviorAnalysis["User Behavior Analysis<br>(Power BI/Azure Analysis Services)"]
   AnonymizedData --> SystemPerformance["System Performance Analysis<br>(Azure Monitor)"]
   AnonymizedData --> FeatureDevelopment["Feature Development<br>(Azure Machine Learning)"]
   AnonymizedData --> ComplianceReporting["Compliance & Reporting<br>(Azure Compliance Center)"]
  
   %% Data Collection
   DataCollection["Data Collection<br>(Azure Data Factory)"] --> RawUserQueries
   DataCollection --> UserFeedback
   DataCollection --> UsageMetrics
   DataCollection --> DataSourceUsage


   %% Model Improvement Cycle
   ModelTraining --> LLM


   class AnonymizationService,AnonymizedData,UserFeedback,UsageMetrics,DataSourceUsage,Infrastructure,DataCollection,FeedbackAnalysis,PerformanceOptimization,DataIntegrationOptimization Azure;
   class RAG,LLM,ModelTraining,UserBehaviorAnalysis,SystemPerformance,FeatureDevelopment,ComplianceReporting MachineLearning;
   class RawUserQueries ExternalData;

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
```

### AI Database
```mermaid
graph TD
   subgraph ExternalSources["External Data Sources"]
   GoogleDrive["Google Drive<br>Slack<br>GMail<br>etc"]:::ExternalData
   end

   AzureFunctions["Azure Functions<br>Data Processing"]:::Azure
   CognitiveSearch["Azure Cognitive Search<br>Indexing & AI Enrichment"]:::Azure

   BlobStorage["Azure Blob Storage<br>Raw & Processed Data"]:::Azure
   CosmosDB["Azure Cosmos DB<br>Operational Data"]:::Azure

   SearchAPI["Azure Cognitive Search<br>API"]:::Azure

   GoogleDrive --> AzureFunctions
   AzureFunctions -->|Data transformation & enrichment| CognitiveSearch
   CognitiveSearch -->|Indexed data| BlobStorage
   AzureFunctions -->|Operational metadata| CosmosDB
   CognitiveSearch -->|Searchable index| SearchAPI
   BlobStorage -->|Backup - Raw data| CosmosDB

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
```

### Client Requests
```mermaid
graph TD
   ClientRequests[Client Requests] -->|API Calls| AzureAPIManagement["Azure API Management"]
   AzureAPIManagement -->|Routes Requests| AKS["Azure Kubernetes Service (AKS)"]
   AKS -->|Hosts| GenericLLM[Generic LLM]
   GenericLLM --> GenerateResponses[Generate Responses]
   AzureAPIManagement -->|Secured by| AzureVNet["Azure Virtual Network & Private Link"]

   class AzureAPIManagement,AKS,AzureVNet Azure;
   class GenericLLM MachineLearning;
   class ClientRequests,GenerateResponses ProcessFlow;

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
```

### Security
```mermaid
graph TD
   AzureAD["Azure Active Directory (AAD)"] -->|Manages Identities| RBAC["Role-Based Access Control (RBAC)"]
   AzureAD -->|B2B| DataIsolationSecurity["Data Isolation & Security"]
   RBAC -->|Enforces Access| AzureResources[Azure Resources]
   DataIsolationSecurity --> AzureResources
   AzureResources -->|Protected by| AzureKeyVault["Azure Key Vault"]
   AzureResources -.->|Monitored by| AzureMonitorSentinel["Azure Monitor & Azure Sentinel"]
   AzureResources -->|Governed by| AzurePolicyBlueprints["Azure Policy & Blueprints"]

   class AzureAD,AzureKeyVault,AzureMonitorSentinel,AzurePolicyBlueprints,RBAC,DataIsolationSecurity Security;
   class AzureResources Azure;

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
```

## External Integrations
### Google Drive
```mermaid
graph TD
   subgraph Azure Cloud
   Functions[Azure Functions<br>Timer Trigger]
   LogicApps["Azure Logic Apps/<br>Durable Functions<br>Workflow Orchestration"]
   BlobStorage[Function Metadata Storage<br>Azure Blob Storage]
   SQLDB[RAG Database<br>Azure AI Search]
   end

   subgraph Google Cloud
   DriveAPI[Google Drive API<br>Changes List]
   end

   ServiceAcc[Service Account<br>with Domain-Wide Delegation] -->|Authenticates| DriveAPI
   Functions -->|Scheduled Polling| DriveAPI
   DriveAPI -->|Fetch Changes| Functions
   Functions -->|Process & Store Data| BlobStorage
   Functions -->|Update RAG Database| SQLDB
   Functions -->|Workflow Orchestration| LogicApps

   class Functions,LogicApps,BlobStorage,SQLDB Azure;
   class DriveAPI,ServiceAcc ExternalData;

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
```

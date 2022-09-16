[[_TOC_]]
# Task 1 - Create Azure Subscription


## Login to https://azure.microsoft.com/en-in/free/

![image.png](/.attachments/image-f95a4d5a-0e05-439a-9386-3b20db39a1c8.png)

**Click --> Start free**

## Create New Account or Signup using your Github

![image.png](/.attachments/image-514b47ca-bf34-418f-adb6-9db2b99436bc.png)

----------           **I signed up using GitHub**    ------------------------------






================ **END OF TASK 1** =======================================


















# Task 2 - Create DevOps Subscription

## Azure Portal

**Once you signed up - You will be directed to https://portal.azure.com/#home**

## Create Resource Group

Go to --> https://portal.azure.com/#create/Microsoft.ResourceGroup

Create Resource Group

![image.png](/.attachments/image-c60d9147-e235-42fe-9a24-45fa46da4408.png)


## Create DevOps Project

1) Search - DevOps - from the Azure Portal Search**

![image.png](/.attachments/image-cb941f70-2eec-4fe4-97b8-8bc254312e0a.png)

2) Create Organization in Azure DevOps

Go to --> https://dev.azure.com/ --> Select "New Organization"

![image.png](/.attachments/image-48b5d6ae-223b-41b8-85cb-9a982620d0d5.png)

3) Create Project inside the Organization --> Select "New Project"
    - This will create a Repository
    - Wiki
    - Project Board

![image.png](/.attachments/image-23ae4ae3-af8d-437c-8566-4c2dbdf77657.png)

Once created you will see below the console 

![image.png](/.attachments/image-a23b9268-f5b4-4024-9bba-d03220047395.png)


================ **END OF TASK 2** =======================================

# Task 3 - Create ML Workspace Manually (Testing)

## Create ML Workspace

1) Search - "Azure Machine Learning - from the Azure Portal Search**

![image.png](/.attachments/image-47eeb4ed-6551-4c86-9e26-4b5d09c92b32.png)

2) Click on "Create" - Wait for 5-10 minutes till Workspace get created.

![image.png](/.attachments/image-a270ac37-152a-41ca-af00-3d48474b5cf6.png)

3) Open Azure ML Workspace Studio URL

![image.png](/.attachments/image-ad36ab08-3021-4e4c-9a34-822a669de054.png)

## Explore Azure ML Studio

- Check Notebooks

- Data
- Jobs and Experiements
- Model
- Endpoints
- Compute
- Data Stores

## Create Compute Instance
- Go to Manage - Compute

![image.png](/.attachments/image-135cec6e-6ef5-4b2a-a915-8c4f0533e47d.png)

Click Create

## Test Data Information

- Go to Assets --> Data --> Create --> From Local Files

![image.png](/.attachments/image-adccadac-6ecb-4408-8cd9-b7dde6dae715.png)

- Browse and Select the files from local

![image.png](/.attachments/image-c045a665-d441-4774-92f0-210e1565bcce.png)

- You can see the Data Discovered and Preview., Also data schema type

![image.png](/.attachments/image-2ae2dfd4-6474-4a29-b4ee-4f07448c6691.png)

![image.png](/.attachments/image-47d3c4ca-4587-48a8-8211-c91a408730b1.png)

- Enable Checkbox of "Profile the Data Set" and select the Compute created in before steps"

![image.png](/.attachments/image-e5b74e3f-d295-464d-9194-608db441c6ea.png)


================ **END OF TASK 3** =======================================


# Task 4 - Create Service Principal and ML Extension to Azure DevOps

## Create Service Connection

- Go to https://dev.azure.com/<your-organization> --> Select your project

- Select Project Settings

![image.png](/.attachments/image-cf7ba405-1897-436f-9775-702c3cec9140.png)
or 
https://dev.azure.com/<your-organization>/<your-project>/_settings

- Click Service Connection. --> New Service Connection --> Select "Azure Resource Manager"

![image.png](/.attachments/image-08280a9e-30cd-4bbf-ba35-c021422d6f88.png)

- Select "Service Principal (automatic) for Azure DevOps

![image.png](/.attachments/image-a3894f30-c943-4495-8466-8d6d1c2aa53f.png)

- Select "Subscription" - We need this to be created, In Order for Azure DevOps to create the required resources inside the Resource group.

![image.png](/.attachments/image-6004b70f-e84c-4a27-bbf1-2bf02bce8551.png)

- Select "Service Principal (automatic) for Azure DevOps to Azure ML


- Select "Machine Learning Workspace " - We need this to be created, In Order for Azure DevOps to create the resources in the Azure Workspace via Azure Pipeline

![image.png](/.attachments/image-3ecabcd7-0864-490b-9a9c-772fa3d985d7.png)

## Install ML Extension to Azure DevOps Project

- Install Machine Learning Extention to Azure DevOps
  Click on the Highlight red one --> Manage Extension --> Browser Market Place

![image.png](/.attachments/image-bae6f905-9200-4d2e-b179-1a87c490e7ab.png)


Select Machine Learning

![image.png](/.attachments/image-cec4c2ed-b19a-4389-a9cf-2f6b18461607.png)


================ **END OF TASK 4** =======================================

# Task 5 - Create ML Workspace via IaaC using Azure DevOps

## Create Variables

- Go to the Azure Projected created in #Task 2 
- Let us create Required Variables in the Library Section Pipeline

![image.png](/.attachments/image-33914eee-8c79-4a1b-924b-4a8fd69292e8.png)

- Create a Variable group


| AZURE_RM_SVC_CONNECTION |mlops-demo-azure-devops-service-connection  |
|--|--|
| BASE_NAME | mlopsblrws |
|LOCATION|eastus2|
|RESOURCE_GROUP|mlops-demo-blr-resource-group|
|WORKSPACE_NAME|mlops-blr-ws-aml|
|WORKSPACE_SVC_CONNECTION|mlops-aml-service-connection

## Create Pipeline

Click on New Pipeline ![image.png](/.attachments/image-c3f4facd-fb72-4e5c-ac64-c900d159eeb5.png)

- Select "Azure Repos Git"

![image.png](/.attachments/image-919c5d52-34ba-49aa-9151-e45308fc3a55.png)

- Select the Repo and Cli

![image.png](/.attachments/image-66b0da93-25a9-4541-bfef-4cd939155cc8.png)

- Select "Existing Azure Pipeline YAML File"

![image.png](/.attachments/image-cb4ab6dd-2aaa-428c-99ad-a3bbc6a97a33.png)

- Provide the Path of YAML

![image.png](/.attachments/image-ab978842-71f8-4b42-a501-a9c51de3151d.png)

- Run the Pipeline  
![image.png](/.attachments/image-097cbdd5-3622-4ee7-905d-33387ed8c285.png)

## Validate the Results

- Select the Pipeline and go to the Run and Make sure it is GREEN

![image.png](/.attachments/image-236c2e24-fe05-4323-a3e1-984d83867797.png)

Check the Jobs for Pipeline Run logs

- Select the recent logs --> go to Jobs and check the Jobs

![image.png](/.attachments/image-16e3302a-0612-410e-8958-67f7dc406648.png)

================ **END OF TASK 5** =======================================

# Task 6 - Create ML Pipeline Continuous Integration


- Follow the same procedure as above to create a Pipeline but select different path for creating MLOps Pipeline

![image.png](/.attachments/image-a03abc48-ff27-4beb-a099-676240c4b0d6.png)

- Create a Variables.


| **Name** |  **Value**|
|--|--|
| aml.sp | **Get the Object ID from DevOps Service Principle** |
| amlcompute.clusterName |mldemocluster  |
| amlcompute.idleSecondsBeforeScaledown|  300|
| amlcompute.maxNodes | 2 |
| amlcompute.minNodes  |  0|
| amlcompute.vmSize | STANDARD_DS2_V2 |
| azureml.location | eastus2 |
| azureml.resourceGroup | mlops-demo-blr-resource-group |
| azureml.workspaceName | mlops-blr-ws-aml |

- Run the Pipeline - It takes 10 Minutes to execute. 

- Select the Run and Click on "Agent Job 1" - and You can see all Tasks in Pipeline succeeded.

![image.png](/.attachments/image-5a4df59b-228b-4f46-821b-abd0b2a7345e.png)

================ **END OF TASK 6** =======================================


# Task 7 - Create Deployment Pipeline
 
- Go to Azure devops project --> Pipelines --> Releases --> Create New Release

![image.png](/.attachments/image-b9848293-6937-4e79-80dc-a6a1f4bd90c5.png)

- You can select the Artifacts from the pipeline created before. - Click Add and Artifact

![image.png](/.attachments/image-1476f619-ae06-4957-9213-ab863c1be605.png)

- Add a Stage to perform the deployment - The best practice is to Create a Deployment to staging environment as part of (Stage 2 )and if succeed deploy to Prod. 
- For Demo Purpose, I am directly deploying to the Production environment.

- Click Add  - New Agent will be created. - Rename to ML-Deployment-Agent

- Create Variables

| **Name** |  **Value**|
|--|--|
|aks.clusterName |**Select your existing cluster**|
|aks.vmSize| Standard_B2ms|
| azureml.resourceGroup |mlops-demo-blr-resource-group |
| azureml.workspaceName | mlops-blr-ws-aml|
| service.name.prod| insurance-ml-model-prod |
| aks.agentCount| 3 |


- Set the Agent Job 
  1) Rename the Display Name
  2) Agent Pool --> Azure Pipeline
  3) Agent Specification --> Ubuntu-18.04

![image.png](/.attachments/image-2dac1839-6304-40f0-a1ed-6856e7e4e08c.png)

- Click on Add task from the Agent

![image.png](/.attachments/image-4140f1e7-7e52-4b56-aa36-0b384c8a160b.png)

  Search for Python Version

![image.png](/.attachments/image-19cd686a-c342-48bc-abfc-a493d88c944e.png)
  
## AZ CLI ML Extension
- Click on Add task from the Agent -> Search Azure CLI -> Change Display - Add ML Extension
 
![image.png](/.attachments/image-a93e2511-06f6-4b6b-8432-dec20a26e827.png)

   * Inline script - Add below Value
  `az extension add -n azure-cli-ml`

![image.png](/.attachments/image-446a0b61-6ee9-4ffa-bb5d-7d1244bb9555.png)


## AZ CLI ML Extension - Deploy to AKS

- Click on Add task from the Agent -> Search Azure CLI -> Change Display -Deploy to AKS

   * Inline script - Add below Value
  `az ml model deploy -g   $(azureml.resourceGroup) -w $(azureml.workspaceName) -n $(service.name.prod) -f ../metadata/model.json --dc aksDeploymentConfigProd.yml --ic inferenceConfig.yml --ct $(aks.clusterName) --overwrite`


![image.png](/.attachments/image-71954ec0-bdcd-4e96-8e29-0fb0e33c5413.png)

## Create Release
- ![image.png](/.attachments/image-9ff091a3-2f7e-4f61-a6a5-6f8bca9e0a9a.png)

- Create

![image.png](/.attachments/image-2dd1a4b8-7bbf-4b76-8543-80c6ac5857a2.png)

- Validate the Status of Pipeline

![image.png](/.attachments/image-80607ad7-995c-4037-b239-9cd8809c506f.png)

================ **END OF TASK 7** =======================================

# Task 8 - Validate Model Endpoint


- Go to Azure Machine learning Workspace 
- Validate the Model - You can see the New Model Created

![image.png](/.attachments/image-322a2b6e-7933-4ab8-abf7-15249227db3b.png)


- Validate Endpoint.

![image.png](/.attachments/image-97b15371-795d-4b06-8248-1677b68a9ba3.png)

- Validate with test data - Step 1 - Get the Python Code
  * Go to Assets - Endpoints -- Consume - Check Python and Take the code

![image.png](/.attachments/image-888fba93-9e60-4dd2-b4eb-ff1992865b5a.png)

- Validate with test data - Step 1 - Test in Notebook

  * Go to Author - Notebook -- Consume - Create the Notebook file. -> Paste the Python Code. -> Change the Value of the Data as mentioned below --> Run the Cell

Replace the line 8 Data with below Values

`data = {'data': [[0,1,8,1,0,0,1,0,0,0,0,0,0,0,12,1,0,0,0.5,0.3,0.610327781,7,1,-1,0,-1,1,1,1,2,1,65,1,0.316227766,0.669556409,0.352136337,3.464101615,0.1,0.8,0.6,1,1,6,3,6,2,9,1,1,1,12,0,1,1,0,0,1],[4,2,5,1,0,0,0,0,1,0,0,0,0,0,5,1,0,0,0.9,0.5,0.771362431,4,1,-1,0,0,11,1,1,0,1,103,1,0.316227766,0.60632002,0.358329457,2.828427125,0.4,0.5,0.4,3,3,8,4,10,2,7,2,0,3,10,0,0,1,1,0,1]]}`


![image.png](/.attachments/image-a517b1fa-588b-4606-b37f-f70c9d0eb39c.png)


- Monitor using the Application Insights using the Application Insight URL from Endpoints.

* Go to Assets - Endpoints - Details --> Application Insights URL --> Click the URL 

![image.png](/.attachments/image-3ec140a2-05a0-42e8-a256-c0044e928f96.png)

* You can see the Application throughput here.

![image.png](/.attachments/image-84ac8ce0-7b11-4235-8f4c-462e984893e4.png)




================ **END OF LAB** =======================================
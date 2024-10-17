# Introduction

> [!NOTE]
>This is a **10-minute** lab that will give you a hands-on introduction to setting up the environment for the workshop.

## Learning Objectives

By the end of this workshop, you should be able to:
// This is a placeholder for the learning objectives. The objectives should be a bulleted list of the skills that the learner will acquire by completing the lab.

## Lab Scenario
> [!NOTE]
>In this workshop lab, you will:

- Create an Azure Machine Learning Workspace.
 
- Create an Azure Machine Learning Workspace
 

## Lab Outline

### Set up the environment for the workshop

- Create Azure Machine Learning workspace
- Request GPU quotas in Azure subscription
- Set up the project and install the libraries
- Set up project files in Visual Studio Code
 
### Create Azure Machine Learning workspace

Open the Azure portal. https://portal.azure.com/

Type azure machine learning in the search bar at the top of the portal page and select Azure Machine Learning from the options that appear.

![](/lab/Workshop%20Instructions/Lab1_Environment_Setup/images/01-1-type-azml.png)

Select + Create from the navigation menu.

Select New workspace from the navigation menu.

![](./images/01-2-select-new-workspace.png)

Perform the following tasks:

- Select your Azure Subscription.
- Select the Resource group to use (create a new one if needed).
Enter Workspace Name. It must be a unique value.
- Select the Region you'd like to use.
- Select the Storage account to use (create a new one if needed).
- Select the Key vault to use (create a new one if needed).
- Select the Application insights to use (create a new one if needed).
- Select the Container registry to use (create a new one if needed).

![](./images/01-03-fill-AZML.png)

> [!TIP]
> When you create or use a Storage account in Azure Machine Learning, a container named "azureml" is automatically created within the Storage account. This container is used for storing model artifacts, training outputs, and other data generated during the machine learning process. In this tutorial, you will use the "azureml" container to manage and store all the necessary files and outputs related to our machine learning workflows.

 
- Select Review + Create.

- Select Create.


### Request GPU quotas in Azure Subscription
 

In this tutorial, you will learn how to fine-tune and deploy a Phi-3 model, using GPUs. For fine-tuning, you will use the `Standard_NC24ads_A100_v4 GPU`, which requires a quota request. 

For deployment, you will use the `Standard_E4s_v3 CPU`, which does not require a quota request.

> [!NOTE]
> Only Pay-As-You-Go subscriptions (the standard subscription type) are eligible for GPU allocation; benefit subscriptions are not currently supported.


### Request GPU Quotas in your Azure Subscription
 
Request GPU Quotas in Azure Subscription

- Visit [Azure ML Studio](https://ml.azure.com/).

Perform the following tasks to request `Standard NCADSA100v4` Family quota:

- Select Quota from the left side tab.
- Select the Virtual machine family to use. For example, select `Standard NCADSA100v4 Family Cluster Dedicated vCPUs`, which includes the `Standard_NC24ads_A100_v4 GPU.`
- Select the Request quota from the navigation menu.

![](./images/01-04-request-quota.png)

- Inside the Request quota page, enter the New cores limit you'd like to use. For example, 24.

- Inside the Request quota page, select Submit to request the GPU quota.

> [!NOTE]
>You can select the appropriate GPU or CPU for your needs by referring to Sizes for Virtual Machines in Azure document.

 
### Add role assignment

To fine-tune and deploy your models, you must first ceate a User Assigned Managed Identity (UAI) and assign it the appropriate permissions. 

This UAI will be used for authentication during deployment, so it is critical to grant it access to the storage accounts, container registry, and resource group.

In this Lab, you will:

- Create User Assigned Managed Identity(UAI).
- Add Contributor role assignment to Managed Identity.
- Add Storage Blob Data Reader role assignment to Managed Identity.
- Add AcrPull role assignment to Managed Identity.
- Create User Assigned Managed Identity(UAI)

Type managed identities in the search bar at the top of the portal page and select Managed Identities from the options that appear.

![](./images/02-7-type-managed-identities.png)

- Select + Create.
![](./images/02-8-select-create.png)

Perform the following tasks to navigate to Add role assignment page:

- Select your Azure Subscription.
- Select the Resource group to use (create a new one if needed).
- Select the Region you'd like to use.
- Enter the Name. It must be a unique value.

![](./images/02-9-fill-managed-identities-1.png)

- Select Review + create.
- Select + Create.

 
### Add Contributor role assignment to Managed Identity
 

Navigate to the Managed Identity resource that you created.

- Select Azure role assignments from the left side tab.
- Select +Add role assignment from the navigation menu.

Inside Add role assignment page, Perform the following tasks:

- Select the Scope to Resource group.
- Select your Azure Subscription.
- Select the Resource group to use.
- Select the Role to Contributor.
![](./images/02-0-fill-contributor-role.png)

- Select Save.

### Add Storage Blob Data Reader role assignment to Managed Identity

- Type azure storage accounts in the search bar at the top of the portal page and select Storage accounts from the options that appear.

![](./images/02-1-type-storage-accounts.png)

- Select the storage account that associated with the Azure Machine Learning workspace. For example, finetunephistorage.

- Perform the following tasks to navigate to Add role assignment page:

- Navigate to the Azure Storage account that you created.
Select Access Control (IAM) from the left side tab.
- Select + Add from the navigation menu.
- Select Add role assignment from the navigation menu.
![](./images/02-3-add-role.png)

Inside Add role assignment page, Perform the following tasks:

Inside the Role page, type Storage Blob Data Reader in the search bar and select Storage Blob Data Reader from the options that appear.

![](./images/02-4-select-data-reader-role.png)

- Inside the Role page, select Next.
- Inside the Members page, select Assign access to Managed identity.
- Inside the Members page, select + Select members.
- Inside Select managed identities page, select your Azure Subscription.
- Inside Select managed identities page, select the Managed identity to Manage Identity.
- Inside Select managed identities page, select the Manage Identity that you created. For example, finetunephi-managedidentity.
- Inside Select managed identities page, select Select.

![](./images/02-5-select-managed-identity.png)

- Select Review + assign.

### Add AcrPull role assignment to Managed Identity
 

Type container registries in the search bar at the top of the portal page and select Container registries from the options that appear.

![](./images/02-10-type-container-registries.png)

- Select the container registry that associated with the Azure Machine Learning workspace. For example, finetunephicontainerregistries

- Perform the following tasks to navigate to Add role assignment page:

- Select Access Control (IAM) from the left side tab.
- Select + Add from the navigation menu.
- Select Add role assignment from the navigation menu.
- Inside Add role assignment page, Perform the following tasks:
- Inside the Role page, Type AcrPull in the search bar and select AcrPull from the options that appear.
- Inside the Role page, select Next.
- Inside the Members page, select Assign access to Managed identity.
- Inside the Members page, select + Select members.
- Inside Select managed identities page, select your Azure Subscription.
- Inside Select managed identities page, select the Managed identity to Manage Identity.
- Inside Select managed identities page, select the Manage Identity that you created. For example, finetunephi-managedidentity.
- Inside Select managed identities page, select Select.
Select Review + assign.

### Set up the project and install the libraries

Now, you will create a folder to work in and set up a virtual environment to develop a program.

In this exercise, you will

- Create a folder to work inside it.
- Create a virtual environment.
- Install the required packages.

### Create a folder to work inside it

- Open a terminal window and type the following command to create a folder named finetune-phi in the default path.

```bash
mkdir finetune-phi
```

- Type the following command inside your terminal to navigate to the finetune-phi folder you created.

```bash
cd finetune-phi
```
 
- Create a virtual environment

- Type the following command inside your terminal to create a virtual environment named .venv.

```Bash
python -m venv .venv
````

- Type the following command inside your terminal to activate the virtual environment.

```bash
.venv\Scripts\activate.bat
```
 
> [!NOTE]
>If it worked, you should see (.venv) before the command prompt.

 
### Install the required packages

Type the following commands inside your terminal to install the required packages.
  
  ```bash
pip install datasets==2.19.1
pip install transformers==4.41.1
pip install azure-ai-ml==1.16.0
pip install torch==2.3.1
pip install trl==0.9.4
pip install promptflow==1.12.0
``` 

### Set up project files in Visual Studio Code

In this exercise, you will create the essential files for our project. These files include scripts for downloading the dataset, setting up the Azure Machine Learning environment, fine-tuning the Phi-3 model, and deploying the fine-tuned model. You will also create a conda.yml file to set up the fine-tuning environment.

In this exercise, you will:

- Create a download_dataset.py file to download the dataset.
Create a setup_ml.py file to set up the Azure Machine Learning environment.
- Create a fine_tune.py file in the finetuning_dir folder to fine-tune the Phi-3 model using the dataset.
- Create a conda.yml file to setup fine-tuning environment.
- Create a deploy_model.py file to deploy the fine-tuned model.
- Create a integrate_with_promptflow.py file, to integrate the fine-tuned model and execute the model using Prompt flow.
Create a flow.dag.yml file, to set up the workflow structure for Prompt flow.
Create a config.py file to enter Azure information.

> [!NOTE]
>Complete folder structure:
> ```
>└── YourUserName
>.    └── finetune-phi
>.        ├── finetuning_dir
>.        │      └── fine_tune.py
>.        ├── conda.yml
>.        ├── config.py
>.        ├── deploy_model.py
>.        ├── download_dataset.py
>.        ├── flow.dag.yml
>.        ├── integrate_with_promptflow.py
>.        └── setup_ml.py
>```
 
### Create Project Files
 
- Open Visual Studio Code.
- Select File from the menu bar.
- Select Open Folder.
- Select the finetune-phi folder that you created, which is located at C:\Users\yourUserName\finetune-phi.

![](./images/04-1-open-project-folder.png)

- In the left pane of Visual Studio Code, right-click and select New File to create a new file named download_dataset.py.

- In the left pane of Visual Studio Code, right-click and select New File to create a new file named setup_ml.py.

- In the left pane of Visual Studio Code, right-click and select New File to create a new file named deploy_model.py.

![](./images/04-2-create-new-file.png)

- In the left pane of Visual Studio Code, right-click and select New Folder to create a new forder named finetuning_dir.

- In the finetuning_dir folder, create a new file named fine_tune.py.

### Create and Configure conda.yml file

- In the left pane of Visual Studio Code, right-click and select New File to create a new file named conda.yml.

- Add the following code to the conda.yml file to set up the fine-tuning environment for the Phi-3 model.

```yml
name: phi-3-training-env
channels:
  - defaults
  - conda-forge
dependencies:
  - python=3.10
  - pip
  - numpy<2.0
  - pip:
      - torch==2.4.0
      - torchvision==0.19.0
      - trl==0.8.6
      - transformers==4.41
      - datasets==2.21.0
      - azureml-core==1.57.0
      - azure-storage-blob==12.19.0
      - azure-ai-ml==1.16
      - azure-identity==1.17.1
      - accelerate==0.33.0
      - mlflow==2.15.1
      - azureml-mlflow==1.57.0
```

### Create and Configure config.py file

- In the left pane of Visual Studio Code, right-click and select New File to create a new file named config.py.

- Add the following code to the config.py file to include your Azure information.

```Python
# Azure settings
AZURE_SUBSCRIPTION_ID = "your_subscription_id"
AZURE_RESOURCE_GROUP_NAME = "your_resource_group_name" # "TestGroup"

# Azure Machine Learning settings
AZURE_ML_WORKSPACE_NAME = "your_workspace_name" # "finetunephi-workspace"

# Azure Managed Identity settings
AZURE_MANAGED_IDENTITY_CLIENT_ID = "your_azure_managed_identity_client_id"
AZURE_MANAGED_IDENTITY_NAME = "your_azure_managed_identity_name" # "finetunephi-mangedidentity"
AZURE_MANAGED_IDENTITY_RESOURCE_ID = f"/subscriptions/{AZURE_SUBSCRIPTION_ID}/resourceGroups/{AZURE_RESOURCE_GROUP_NAME}/providers/Microsoft.ManagedIdentity/userAssignedIdentities/{AZURE_MANAGED_IDENTITY_NAME}"

# Dataset file paths
TRAIN_DATA_PATH = "data/train_data.jsonl"
TEST_DATA_PATH = "data/test_data.jsonl"

# Fine-tuned model settings
AZURE_MODEL_NAME = "your_fine_tuned_model_name" # "finetune-phi-model"
AZURE_ENDPOINT_NAME = "your_fine_tuned_model_endpoint_name" # "finetune-phi-endpoint"
AZURE_DEPLOYMENT_NAME = "your_fine_tuned_model_deployment_name" # "finetune-phi-deployment"

AZURE_ML_API_KEY = "your_fine_tuned_model_api_key"
AZURE_ML_ENDPOINT = "your_fine_tuned_model_endpoint_uri" # "https://{your-endpoint-name}.{your-region}.inference.ml.azure.com/score"
```

### Add Azure Environment Variables

Perform the following tasks to add the Azure Subscription ID:

- Type subscriptions in the search bar at the top of the portal page and select Subscriptions from the options that appear.

![Type subscriptions in the search bar](./images/05-3-type-subscriptions.png)

- Select the Azure Subscription you are currently using.
Copy and paste your Subscription ID into the config.py file.

![](./images/05-4-find-subscriptionid.png)

- Perform the following tasks to add the Azure Workspace Name:

- Navigate to the Azure Machine Learning resource that you created.

- Copy and paste your account name into the config.py file.

![](./images/05-5-find-AZML-name.png)

- Perform the following tasks to add the Azure Resource Group Name:

- Navigate to the Azure Machine Learning resource that you created.
- Copy and paste your Azure Resource Group Name into the config.py file.

![](./images/05-6-find-AZML-resourcegroup.png)

- Perform the following tasks to add the Azure Managed Identity name

- Navigate to the Managed Identities resource that you created.
- Copy and paste your Azure Managed Identity name into the config.py file.

![](/lab/Workshop%20Instructions/Lab1_Environment_Setup/images/05-9-find-uai.png)

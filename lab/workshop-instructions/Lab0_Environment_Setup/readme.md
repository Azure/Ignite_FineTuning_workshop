# Lab 1. Azure AI Workshop Environment Setup

## Introduction 
> [!NOTE]
>This is a **15-minute** lab that will give you a hands-on introduction to setting up the environment for the workshop.

## Learning Objectives

By the end of this workshop, you should be able to:
// This is a placeholder for the learning objectives. The objectives should be a bulleted list of the skills that the learner will acquire by completing the lab.

## Lab Scenario
> [!NOTE]
>In this workshop lab, you will:

- Setup VScode and necessary frameworks
- Create a new Azure AI Hub
- Create a new Azure AI Project

### Task 
During this lab we will develop a travel companion application that leverages Large Language Models (LLMs) to provide personalized travel recommendations, itinerary planning, and real-time assistance to travellers. The labs will focus on fine-tuning a GPT model using Azure AI and a code-first approach using Python and Microsoft Olive.

We will focus on the specific areas 
- Setting up Azure AI Hub & Project
- Prepare Training Data
- One-Button Fine-Tuning with Azure AI
- Import a pre-trained model into the project.
- Deploy the Fine-Tuned Model
- Test the model by querying travel recommendations and itinerary planning.
- Python code to fine-tune GPT model with the prepared data.
- Use Microsoft Olive for model optimization, including pruning and quantization.
- Evaluate the model's performance and compare it with the Azure-deployed model.
- Evaluate which method provided better performance and insights.
  
### Set up the environment for the workshop on your personal machine

## Setup Local Dev Environment 

## install az cli
'winget install -e --id Microsoft.AzureCLI'

## install az ml extension
'az extension add -n ml'

## verify az ml extension has been installed
`az extension list --output table`

## Install .NET 8 on Windows

- Download .NET 8.0: Visit the official .NET download page +++https://dotnet.microsoft.com+++ and download the .NET 8.0 SDK for Windows
- Run the Installer: Open the downloaded installer and follow the prompts to install the .NET 8.0 SDK
- Restart Your Computer: After installation, restart your computer to complete the setup

**Optional Steps:**
- Install the .NET Runtime: If you need to run .NET applications, you might also want to install the .NET Runtime and ASP.NET Core Runtime
- Install Visual Studio Code: If you haven't already, you can install Visual Studio Code and the C# Dev Kit extension for a better development experience

## Installing Visual Studio Code on Windows

Download VS Code: Visit the VS Code download page and download the installer for Windows +++https://vscode.microsoft.com+++

- Run the Installer: Open the downloaded installer and follow the prompts to install VS Code
- Launch VS Code: Once installed, you can open VS Code from the start menu

## Installing the Python Extension
- Open VS Code: Launch VS Code
- Open the Extensions View: Press Ctrl+Shift+X or click on the Extensions icon in the Activity Bar on the side of the window
- Search for Python: In the Extensions view, search for "Python" and click on the Python extension by Microsoft
- Install the Extension: Click the "Install" button to install the Python extension
- Select Python Interpreter: After installation, you may need to select your Python interpreter by clicking on the Python version in the bottom left corner and choosing the appropriate interpreter.

## Installing the .NET Extension
- Open the Extensions View: Press Ctrl+Shift+X or click on the Extensions icon in the Activity Bar
- Search for .NET: In the Extensions view, search for ".NET" and click on the C# Dev Kit extension by Microsoft
- Install the Extension: Click the "Install" button to install the .NET extension.
- Install .NET SDK: Follow the prompts to install the .NET SDK if it is not already installed

## Setting Up Your Environment
Create a Project: Open a new folder or create a new project

- Initialize a .NET Project: Open a terminal in VS Code (Ctrl+ or Ctrl+Shift+M) and run the command dotnet new console to create a new .NET console project
- Run the Project: Run the project by typing dotnet run in the terminal

You should now have a working setup with VS Code, the Python extension, and the .NET extension. If you encounter any issues or need further assistance, feel free to ask!

# Create an AI Hub and Project in the Azure AI

You start by creating an Azure AI project within an Azure AI hub:

1. In a web browser, open +++https://ai.azure.com+++ and sign in using your Azure credentials.
1. Select the **Home** page, then select **+ New project**.
1. In the **Create a new project** wizard,create a project with the following settings:
    - **Project name**: *A unique name for your project*
    - **Select Customize**
    - **Hub**: *Create a new hub with the following settings:*
    - **Hub name**: *A unique name*
    - **Subscription**: *Your Azure subscription*
    - **Resource group**: *A new resource group*
    - **Location**: Choose one of the following regions **North Central US**, **Sweden Central**\*
    - **Connect Azure AI Services or Azure OpenAI**: (New) *Autofills with your selected hub name*
    - **Connect Azure AI Search**: Skip connecting

    > \* Azure OpenAI resources are constrained at the tenant level by regional quotas. The listed regions in the location helper include default quota for the model type(s) used in this exercise. Randomly choosing a region reduces the risk of a single region reaching its quota limit. In the event of a quota limit being reached later in the exercise, there's a possibility you may need to create another resource in a different region. Learn more about model availability per region +++https://learn.microsoft.com/azure/ai-services/openai/concepts/models#gpt-35-turbo-model-availability+++

1. Review your configuration and create your project.
1. Wait for your project to be created.

**Note:** To create a hub, you must have Owner or Contributor permissions on the selected resource group. It's recommended to share a hub with your team. This lets you share configurations like data connections with all projects, and centrally manage security settings and spend. For more options to create a hub, see how to create and manage an Azure AI hub. A project name must be unique between projects that share the same hub..

**Tip:** Especially for getting started it's recommended to create a new resource group for your project. This allows you to easily manage the project and all of its resources together. When you create a project, several resources are created in the resource group, including a hub, a container registry, and a storage account.

Once a project is created, you can access the playground, tools, and other assets in the left navigation panel.

On the project Settings page you can find information about the project, such as the project name, description, and the hub that hosts the project. You can also find the project ID, which is used to identify the project via SDK or API.

![Screenshot of an AI project settings page.](./images/project-settings.png)

- Name: The name of the project corresponds to the selected project in the left panel.
- Hub: The hub that hosts the project.
- Location: The location of the hub that hosts the project. For supported locations, see Azure AI regions.
- Subscription: The subscription that hosts the hub that hosts the project.
- Resource group: The resource group that hosts the hub that hosts the project.
- Select Manage in the Azure portal to navigate to the project resources in the Azure portal.



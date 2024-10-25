# Lab 3. Fine-tune a language model for chat completion in the Azure AI Studio

## Introduction

In this exercise, you'll fine-tune a language model with the Azure AI Studio that you want to use for a custom chat application scenario. You'll compare the fine-tuned model with a base model to assess whether the fine-tuned model fits your needs better.

You work for a travel agency and you're developing a chat application to help people plan their vacations. The goal is to create a simple and inspiring chat that suggests destinations and activities. Since the chat isn't connected to any data sources, it should **not** provide specific recommendations for hotels, flights, or restaurants to ensure trust with your customers.

This exercise will take approximately **60** minutes.


## Learning Objectives
By the end of this workshop, you should be able to:
1. Explore the model catalog in Azure AI Studio.
1. Deploy a model from the model catalog
1. Fine-tune and deploy the GPT model in Azure AI Studio
1. Test the fine-tuned model

## Lab Scenario
The lab scenario of this lab, you will fine-tune the GPT3.5 model using Azure AI Studio one button fine tuning and Azure Model Catalog.

## Lab Outline
This lab consists of the following exercises:
1. Fine-tune and Deploy the GPT model in Azure AI Studio
1. The Azure AI Studio’s model catalog serves as a central repository where you can explore and use a variety of models, facilitating the creation of your generative AI scenario.

# Fine-tune a language model for chat completion in the Azure AI Studio

When you want a language model to behave a certain way, you can use prompt engineering to define the desired behavior. When you want to improve the consistency of the desired behavior, you can opt to fine-tune a model, comparing it to your prompt engineering approach to evaluate which method best fits your needs.

## Create an AI hub and project in the Azure AI Studio

You start by creating an Azure AI Studio project within an Azure AI hub:

1. In a web browser, open [https://ai.azure.com](https://ai.azure.com) and sign in using your Azure credentials.
1. Select the **Home** page, then select **+ New project**.
1. In the **Create a new project** wizard, create a project with the following settings:
    - **Project name**: *A unique name for your project*
    - **Hub**: *Create a new hub with the following settings:*
    - **Hub name**: *A unique name*
    - **Subscription**: *Your Azure subscription*
    - **Resource group**: *A new resource group*
    - **Location**: Select **Help me choose** and then select **gpt-35-turbo** in the Location helper window and use the recommended region\*
    - **Connect Azure AI Services or Azure OpenAI**: *Create a new connection*
    - **Connect Azure AI Search**: Skip connecting

    > \* Azure OpenAI resources are constrained at the tenant level by regional quotas. The listed regions in the location helper include default quota for the model type(s) used in this exercise. Randomly choosing a region reduces the risk of a single region reaching its quota limit. In the event of a quota limit being reached later in the exercise, there's a possibility you may need to create another resource in a different region. Learn more about [model availability per region](https://learn.microsoft.com/azure/ai-services/openai/concepts/models#gpt-35-turbo-model-availability)

1. Review your configuration and create your project.
1. Wait for your project to be created.

## Fine-tune a GPT-3.5 model

As fine-tuning a model takes some time to complete, you'll start the fine-tuning job first. Before you can fine-tune a model, you need a dataset.

1. Save the training dataset as JSONL file locally: https://raw.githubusercontent.com/MicrosoftLearning/mslearn-ai-studio/main/data/travel-finetune.jsonl
1. Navigate to the **Fine-tuning** page under the **Tools** section, using the menu on the left.
1. Select the button to add a new fine-tune model, select the `gpt-35-turbo` model, and select **Confirm**.
1. **Fine-tune** the model using the following configuration:
    - **Model version**: *Select the default version*
    - **Model suffix**: `ft-travel`
    - **Azure OpenAI connection**: *Select the connection that was created when you created your hub*
    - **Training data**: Upload files
    - **Upload file**: Select the JSONL file you downloaded in a previous step.

    > **Tip**: You don't have to wait for the data processing to be completed to continue to the next step.

    - **Validation data**: None
    - **Task parameters**: *Keep the default settings*
1. Fine-tuning will start and may take some time to complete.

> **Note**: Fine-tuning and deployment can take some time, so you may need to check back periodically. You can already continue with the next step while you wait.

## Chat with a base model

While you wait for the fine-tuning job to complete, let's chat with a base GPT 3.5 model to assess how it performs.

1. Navigate to the **Deployments** page under the **Components** section, using the menu on the left.
1. Select the **+ Deploy model** button, and select the **Deploy base model** option.
1. Deploy a `gpt-35-turbo` model, which is the same type of model you used when fine-tuning.
1. When deployment is completed, navigate to the **Chat** page under the **Project playground** section.
1. Select your deployed `gpt-35-model` base model in the setup deployment.
1. In the chat window, enter the query `What can you do?` and view the response.
    The answers are very generic. Remember we want to create a chat application that inspires people to travel.
1. Update the system message with the following prompt:
    ```
    You are an AI assistant that helps people plan their holidays.
    ```
1. Select **Save**, then select **Clear chat**, and ask again `What can you do?`
    As a response, the assistant may tell you that it can help you book flights, hotels and rental cars for your trip. You want to avoid this behavior.
1. Update the system message again with a new prompt:

    ```
    You are an AI travel assistant that helps people plan their trips. Your objective is to offer support for travel-related inquiries, such as visa requirements, weather forecasts, local attractions, and cultural norms.
    You should not provide any hotel, flight, rental car or restaurant recommendations.
    Ask engaging questions to help someone plan their trip and think about what they want to do on their holiday.
    ```

1. Select **Save**, and **Clear chat**.
1. Continue testing your chat application to verify it doesn't provide any information that isn't grounded in retrieved data. For example, ask the following questions and explore the model's answers:
   
     `Where in Rome should I stay?`
    
    `I'm mostly there for the food. Where should I stay to be within walking distance of affordable restaurants?`
    
    `Give me a list of five hotels in Trastevere.`

    The model may provide you with a list of hotels, even when you instructed it not to give hotel recommendations. This is an example of inconsistent behavior. Let's explore whether the fine-tuned model performs better in these cases.

1. Navigate to the **Fine-tuning** page under **Tools** to find your fine-tuning job and its status. If it's still running, you can opt to continue manually evaluating your deployed base model. If it's completed, you can continue with the next section.

## Deploy the fine-tuned model

When fine-tuning has successfully completed, you can deploy the fine-tuned model.

1. Select the fine-tuned model. Select the **Metrics** tab and explore the fine-tune metrics.
1. Deploy the fine-tuned model with the following configurations:
    - **Deployment name**: *A unique name for your model, you can use the default*
    - **Deployment type**: Standard
    - **Tokens per Minute Rate Limit (thousands)**: 5K
    - **Content filter**: Default
1. Wait for the deployment to be complete before you can test it, this may take a while.

## Test the fine-tuned model

Now that you deployed your fine-tuned model, you can test the model like you can tested the your deployed base model.

1. When the deployment is ready, navigate to the fine-tuned model and select **Open in playground**.
1. Update the system message with the following instructions:

    ```
    You are an AI travel assistant that helps people plan their trips. Your objective is to offer support for travel-related inquiries, such as visa requirements, weather forecasts, local attractions, and cultural norms.
    You should not provide any hotel, flight, rental car or restaurant recommendations.
    Ask engaging questions to help someone plan their trip and think about what they want to do on their holiday.
    ```

1. Test your fine-tuned model to assess whether its behavior is more consistent now. For example, ask the following questions again and explore the model's answers:
   
     `Where in Rome should I stay?`
    
    `Where should i go on Holiday for my 30th Birthday and I love active Sight seeing trips?`
    


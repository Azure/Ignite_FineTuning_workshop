# Lab 3. Fine-tune a language model for chat completion in the Azure AI

## Introduction

You work for a travel agency and you're developing a chat application to help people plan their vacations. The goal is to create a simple and inspiring chat that suggests destinations and activities.

When you want a language model to behave a certain way, you can use prompt engineering to define the desired behavior. When you want to improve the consistency of the desired behavior, you can opt to fine-tune a model, comparing it to your prompt engineering approach to evaluate which method best fits your needs.

In this exercise, you'll fine-tune a language model with the Azure AI that you want to use for a custom chat application scenario. You'll compare the fine-tuned model with a base model to assess whether the fine-tuned model fits your needs better.

Imagine you work for a travel agency and you're developing a chat application to help people plan their vacations. The goal is to create a simple and inspiring chat that suggests destinations and activities. Since the chat isn't connected to any data sources, it should not provide specific recommendations for hotels, flights, or restaurants to ensure trust with your customers.
This exercise will take approximately **40** minutes.


## Learning Objectives
By the end of this workshop, you should be able to:
1. Explore the model catalog in Azure AI.
1. Deploy a model from the model catalog
1. Fine-tune and deploy the GPT model in Azure AI.
1. Test the fine-tuned model

## Lab Scenario
The lab scenario of this lab, you will fine-tune the GPT3.5 model using Azure AI one button fine tuning and Azure Model Catalog.

## Lab Outline
This lab consists of the following exercises:
1. Fine-tune and Deploy the GPT model in Azure AI
1. The Azure AI model catalog serves as a central repository where you can explore and use a variety of models, facilitating the creation of your generative AI scenario.

# Fine-tune a language model for chat completion in the Azure AI

When you want a language model to behave a certain way, you can use prompt engineering to define the desired behavior. When you want to improve the consistency of the desired behavior, you can opt to fine-tune a model, comparing it to your prompt engineering approach to evaluate which method best fits your needs.

## Open your AI hub and project in the Azure AI

You start by using your Azure AI project within your Azure AI hub previous created in Lab1. If you have not created your AI Hub see [Lab1_Environmental Setup](../Lab1_Environment_Setup/readme.md)


## Fine-tuning a Large Language Model using Microsoft AI UI Based Fine Tuning 

## Task: Fine-tune a GPT-3.5 model

As fine-tuning a model takes some time to complete, you'll start the fine-tuning job first. Before you can fine-tune a model, you need a dataset based on our scenario we have provided a sample dataset based on the travel agent scenario. In [Lab2.Data_Preparation](../Lab2_Data_Preparation/readme.md) you should of also created datasets, please select a jsonl file.

> **Note**: If you dont have a prepared training dataset as JSONL file locally:
> you can download this sample
> [https://raw.githubusercontent.com/Azure/Ignite_FineTuning_workshop/refs/heads/main/lab/workshop-instructions/Lab5-Optimize-Model/data/data_sample_travel.jsonl) 

1. Open up [Azure AI](https://ai.azure.com)
1. Navigate to the **Fine-tuning** page under the **Tools** section, using the menu on the left.
1. Select the button to add a new fine-tune model, select the model you wish to fine tune `gpt-35-turbo` model, and select **Confirm**.
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

While you wait for the fine-tuning job to complete, let's chat with a base GPT 3.5 model to assess how it performs. Since the chat isn't connected to any data sources, it should **not** provide specific recommendations for hotels, flights, or restaurants to ensure trust with your customers.

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



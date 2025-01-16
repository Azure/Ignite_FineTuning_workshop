
[![GitHub contributors](https://img.shields.io/github/contributors/azure/Ignite_FineTuning_workshop.svg)](https://GitHub.com/microsoft/azure/Ignite_FineTuning_workshop/graphs/contributors/?WT.mc_id=aiml-00003-leestott)
[![GitHub issues](https://img.shields.io/github/issues/azure/Ignite_FineTuning_workshop.svg)](https://GitHub.com/microsoft/azure/Ignite_FineTuning_workshop/issues/?WT.mc_id=aiml-00003-leestott)
[![GitHub pull-requests](https://img.shields.io/github/issues-pr/azure/Ignite_FineTuning_workshop.svg)](https://GitHub.com/azure/Ignite_FineTuning_workshop/pulls/?WT.mc_id=aiml-00003-leestotto)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com?WT.mc_id=aiml-00003-leestott)

[![GitHub watchers](https://img.shields.io/github/watchers/azure/Ignite_FineTuning_workshop.svg?style=social&label=Watch)](https://GitHub.com/azure/Ignite_FineTuning_workshop/watchers/?WT.mc_id=aiml-00003-leestott)
[![GitHub forks](https://img.shields.io/github/forks/azure/Ignite_FineTuning_workshop.svg?style=social&label=Fork)](https://GitHub.com/azure/Ignite_FineTuning_workshop/network/?WT.mc_id=aiml-00003-leestott)
[![GitHub stars](https://img.shields.io/github/stars/azure/Ignite_FineTuning_workshop?style=social&label=Star)](https://GitHub.com/azure/Ignite_FineTuning_workshop/stargazers/?WT.mc_id=aiml-00003-leestott)
[![Azure AI Community Discord](https://dcbadge.vercel.app/api/server/ByRwuEEgH4)](https://discord.com/invite/ByRwuEEgH4?WT.mc_id=aiml-00003-leestott)

# Unlocking NLP Potential: Fine-Tuning with Microsoft Olive PRE016

[Slide Deck](./session-delivery-resources/PRE016-Ignite2024.pdf)

## Fine-Tuning Workshop

This repository is for the Ignite 2024 PreDay Workshop on Fine Tuning Large Language Models

![session banner](./Images/banner.png)

## Session Description

Abstract: Join us for an exclusive workshop on fine-tuning pre-trained language models using Microsoft Olive. Optimizes the fine-tuning process both in the cloud and locally. Deep dive into advanced techniques, gain hands-on experience, and practical insights to elevate your NLP projects. Achieve state-of-the-art performance and unlock new possibilities in NLP. Enhance your skills and stay ahead in the rapidly evolving field of NLP.

## Session Overview 

**Introduction and Overview (15 minutes)**
- Welcome and objectives
- Overview of Fine Tuning 
- Solution Scenario 


**0. Setting Up the Environment (15 minutes)**
- Step-by-step guide to setting your VScode and CLI
- This step has been completed if your using Skillable labs

| Lab # | Title | Description |
| ----- | ------ |----------- |
| 0 | Set up | Learn how to set-up your Azure resources for this lab. |

**1. Login to Azure AI and Setup Compute Node (15 minutes)**
- Setting up a Cloud GPU environment

| Lab # | Title | Description |
| ----- | ------ |----------- |
| 1 | Set up | Login to your AI Hub and Project and deploy a GPU Compute resource. |

**2. Data Preperation (15 minutes)**
- Creating Synthentic Data using GPTs

| Lab # | Title | Description |
| ----- | ------ |----------- |
| 2 | Data Prep | Learn how to prepare data for Finetuning and evaluation. |

**3. Fine-Tuning Basics (40 minutes)**
- Understanding pre-trained models
- Introduction to fine-tuning techniques
- Hyperparameter tuning
- Data augmentation strategies
- Hands-on exercise: Implementing advanced techniques
- Hands-on exercise: Fine-tuning a simple model

| Lab # | Title | Description |
| ----- | ------ |----------- |
| 3 | Finetuning with Azure AI Foundry | Learn how to finetune with Azure AI Foundry|

**4. Deployment of a Model (45 minutes)**
- Deployment strategies on Azure
- Local deployment considerations
- Deploy the Model: Once fine-tuned, deploy the model using the managed compute deployment option
- Create an Endpoint: Set up an endpoint for real-time inference
- Test the Endpoint: Use sample data to test the deployed model and ensure it's working correctly

| Lab # | Title | Description |
| ----- | ------ |----------- |
| 4 | Deploying models to a cloud endpoint | Learn how to deploy models to a cloud endpoint for inference using Azure AI Foundry. |

**5. Optimizing Performance (30 minutes)**
- Monitoring and evaluating model performance
- Using Microsoft Olive for optimization
- Hands-on exercise: Performance tuning

| Lab # | Title | Description |
| ----- | ------ |----------- |
| 5 | Optimize your model for Inference using Microsoft Olive | Learn to optimize your model for on-device inference using Olive. This will include quantization methods and ONNX runtime optimizations. |

**6. Evaluation of Fine-Tuned Models (45 minutes)**
- Evaluating the fine-tuned model
- Responsible AI considerations
- Hands-on exercise: Evaluating the model

| Lab # | Title | Description |
| ----- | ------ |----------- |
| 6 | How to evaluate AI models | In this lab we show you how to evaluate your models to ensure they give trustworthy and safe responses. |

**7. Consumption of the Model (30 minutes)**
- Using .NET Aspire Application to consumed the fine tuned model
- Optimize the model for specific hardware

| Lab # | Title | Description |
| ----- | ------ |----------- |
| 7 | Bring it all together in an app | In this lab we build an application that consumes the AI models you trained and optimized in previous labs. The application will call 2 different models: 1 model will be in the cloud and the other will be on-device. |

**8. Clean Up**
- Remove Azure Resources and Cleanup Resource Groups

| Lab # | Title | Description |
| ----- | ------ |----------- |
| 8 | Clean up | In this lab, we clean up all the resources.

**9. Q&A and Wrap-Up (15 minutes)**
- Open floor for questions
- Recap of key takeaways
- Next steps and additional resources



### Duration
4 hours

### [Slide Deck](./session-delivery-resources/PRE016-Ignite2024.pdf)

## Learning Outcomes
* Understand how to fine tune Language Models
* Create synethic data 
* Fine-Tuning techniques and best practices​

## Technology Used
* Azure AI
* Azure Machine Learning
* Microsoft Olive
* Microsoft ONNX Runtime

## Additional Resources and Continued Learning

| Resources          | Links                             | Description        |
|:-------------------|:----------------------------------|:-------------------|
| Session Slides | [View](https://aka.ms/..) | Review the slides presented during the workshop at your own pace |


## Content Owners
<!-- TODO: Add yourself as a content owner
1. Change the src in the image tag to {your github url}.png
2. Change INSERT NAME HERE to your name
3. Change the github url in the final href to your url. -->


<table>
<tr>
    <td align="center"><a href="http://learnanalytics.microsoft.com">
        <img src="https://github.com/leestott.png" width="100px;" alt="Lee Stott"/><br />
        <sub><b> Lee Stott
</b></sub></a><br />
            <a href="https://github.com/leestott" title="talk">📢</a> 
    </td>
    <td align="center"><a href="http://learnanalytics.microsoft.com">
        <img src="https://github.com/kinfey.png" width="100px;" alt="Kinfey Lo"/><br />
        <sub><b>Kinfey Lo
</b></sub></a><br />
</td>
    <td align="center"><a href="http://learnanalytics.microsoft.com">
        <img src="https://github.com/samuel100.png" width="100px;" alt="Sam Kemp"/><br />
        <sub><b>Sam Kemp
</b></sub></a><br />
            <a href="https://github.com/bethanyjep" title="talk">📢</a> 
    </td>
</tr></table>

## Responsible AI 

Microsoft is committed to helping our customers use our AI products responsibly, sharing our learnings, and building trust-based partnerships through tools like Transparency Notes and Impact Assessments. Many of these resources can be found at [https://aka.ms/RAI](https://aka.ms/RAI).
Microsoft’s approach to responsible AI is grounded in our AI principles of fairness, reliability and safety, privacy and security, inclusiveness, transparency, and accountability.

Large-scale natural language, image, and speech models - like the ones used in this sample - can potentially behave in ways that are unfair, unreliable, or offensive, in turn causing harms. Please consult the [Azure OpenAI service Transparency note](https://learn.microsoft.com/legal/cognitive-services/openai/transparency-note?tabs=text) to be informed about risks and limitations.

The recommended approach to mitigating these risks is to include a safety system in your architecture that can detect and prevent harmful behavior. [Azure AI Content Safety](https://learn.microsoft.com/azure/ai-services/content-safety/overview) provides an independent layer of protection, able to detect harmful user-generated and AI-generated content in applications and services. Azure AI Content Safety includes text and image APIs that allow you to detect material that is harmful. We also have an interactive Content Safety Studio that allows you to view, explore and try out sample code for detecting harmful content across different modalities. The following [quickstart documentation](https://learn.microsoft.com/azure/ai-services/content-safety/quickstart-text?tabs=visual-studio%2Clinux&pivots=programming-language-rest) guides you through making requests to the service.

Another aspect to take into account is the overall application performance. With multi-modal and multi-models applications, we consider performance to mean that the system performs as you and your users expect, including not generating harmful outputs. It's important to assess the performance of your overall application using [generation quality and risk and safety metrics](https://learn.microsoft.com/azure/ai-studio/concepts/evaluation-metrics-built-in).

You can evaluate your AI application in your development environment using the [prompt flow SDK](https://microsoft.github.io/promptflow/index.html). Given either a test dataset or a target, your generative AI application generations are quantitatively measured with built-in evaluators or custom evaluators of your choice. To get started with the prompt flow sdk to evaluate your system, you can follow the [quickstart guide](https://learn.microsoft.com/azure/ai-studio/how-to/develop/flow-evaluate-sdk). Once you execute an evaluation run, you can [visualize the results in Azure AI Studio](https://learn.microsoft.com/azure/ai-studio/how-to/evaluate-flow-results).


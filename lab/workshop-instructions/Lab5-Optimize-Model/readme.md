# Lab 5. Optimize AI models for on-device inference

## Introduction 

> [!IMPORTANT]
> This lab requires an **Nvidia A10 or A100 GPU** with associated drivers and CUDA toolkit (version 12+) installed.

> [!NOTE]
> This is a **30-minute** lab that will give you a hands-on introduction to the core concepts of optimizing models for on-device inference using OLIVE.

## Learning Objectives

By the end of this lab, you will be able to use OLIVE to:

- Quantize an AI Model using the AWQ quantization method.
- Fine-tune an AI model for a specific task.
- Generate LoRA adapters (fine-tuned model) for efficient on-device inference on the ONNX Runtime.

### What is OLIVE

OLIVE (ONNX LIVE) is a model optimization toolkit with accompanying CLI that enables you to ship models for the [ONNX runtime](https://onnxruntime.ai) with quality and performance.

![Olive Flow](./images/olive-flow.png)

The input to OLIVE is typically a PyTorch or Hugging Face model and the output is an optimized ONNX model that is executed on a device (deployment target) running the ONNX runtime. OLIVE will optimize the model for the deployment target's AI accelerator (NPU, GPU, CPU) provided by a hardware vendor such as Qualcomm, AMD, Nvidia or Intel.

OLIVE executes a *workflow*, which is an ordered sequence of individual model optimization tasks called *passes* - example passes include: model compression, graph capture, quantization, graph optimization. Each pass has a set of parameters that can be tuned to achieve the best metrics, say accuracy and latency, that are evaluated by the respective evaluator. OLIVE employs a search strategy that uses a search algorithm to auto-tune each pass one by one or set of passes together.

#### Benefits of OLIVE

- **Reduce frustration and time** of trial-and-error manual experimentation with different techniquies for graph optimization, compression and quantization. Define your quality and performance constraints and let OLIVE automatically find the best model for you.
- **40+ built-in model optimization components** covering cutting edge techniques in quantization, compression, graph optimization and finetuning.
- **Easy-to-use CLI** for common model optimization tasks. For example, olive quantize, olive auto-opt, olive finetune.
- Model packaging and deployment built-in.
- Supports generating models for **Multi LoRA serving**.
- Construct workflows using YAML/JSON to orchestrate model optimization and deployment tasks.
- **Hugging Face** and **Azure AI** Integration.
- Built-in **caching** mechanism to **save costs**.

## Lab Instructions
> [!NOTE]
> Please ensure you have provision your Azure AI Studio Hub and Project as per Lab 1.

### Step 2: Clone this repo

On your Azure AI Compute Instance, run the following commands in a terminal window. In VS Code, you can open a new terminal with **Ctrl+j**.

```bash
cd ~/cloudfiles
git clone https://github.com/Azure/Ignite_FineTuning_workshop.git
```

### Step 3: Open Folder in VS Code

In your Azure AI VS Code, open the clone repo folder by selecting **File** > **Open Folder**.

Choose the following path: `lab/workshop-instructions/lab5-optimize-model`

### Step 4: Install dependencies

Open a terminal window in VS Code in your Azure AI Compute Instance (tip: **Ctrl+j**) and execute:

```bash
conda create -n -y olive-ai python=3.11
conda activate olive-ai
pip install -r requirements.txt
sudo apt-get -y install cudnn9-cuda-12
```

### Step 5: Execute OLIVE commands 

#### Option A: Execute commands in Notebook

If you prefer to use Jupyter, you can open the `olive-optimization.ipynb` and follow the instructions contained in the Python Notebook.

#### Option B: Execute commands from the command line

Open a terminal window in VS Code in your Azure AI Compute Instance (tip: **Ctrl+j**) and activate the `olive-ai` conda environment:

```bash
conda activate olive-ai
```

Next, execute the following scripts...

1. Execute [Active Aware Quantization (AWQ)](https://arxiv.org/abs/2306.00978) using:
    
    ```bash
    ./scripts/01-quantize.sh
    ```
    
    It takes **~10mins** to complete the AWQ quantization.

1. Fine-tune the quantized model using:
    
    ```bash
    ./scripts/02-finetune.sh
    ```
    
    It takes **~10mins** to complete the Fine-tuning (depending on the number of epochs).

1. Generate adapters and optimize for the ONNX runtime:
    
    ```bash
    ./scripts/03-gen-adapters.sh
    ```
    
    It takes **~2mins** to complete the adapter extraction and ONNX optimization.

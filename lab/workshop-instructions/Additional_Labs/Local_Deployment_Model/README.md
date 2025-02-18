# Using ONNX Runtime GenAI to run SLM ONNX model in your local env

> [!NOTE]
>This is a **30-minute** workshop that will give you a hands-on introduction to run SLM onnx model with ORT GenAI .NET

## Learning Objectives


By the end of this workshop, you should be able to:
1. Know basic knowledge of ONNX Runtime GenAI 
2. Compile ONNX Runtime GenAI with CMake
3. Run local model with .NET


### Learn ONNX Runtime GenAI

Run generative AI models with ONNX Runtime.

See the source code here: [https://github.com/microsoft/onnxruntime-genai](https://github.com/microsoft/onnxruntime-genai)

This library provides the generative AI loop for ONNX models, including inference with ONNX Runtime, logits processing, search and sampling, and KV cache management.

Users can call a high level generate() method, or run each iteration of the model in a loop, generating one token at a time, and optionally updating generation parameters inside the loop.

It has support for greedy/beam search and TopP, TopK sampling to generate token sequences and built-in logits processing like repetition penalties. You can also easily add custom scoring.


### Running local onnx model with ONNX Runtime GenAI 

Microsoft Phi-3.5 allows us to run smoothly in different edge devices. The local edge devices can have the computing power of CPU, GPU, and NPU. We hope that you can use the local CPU to run local ONNX model 

1. Set up dev env

   - Visual Studio Code .NET Extension Pack 
   - .NET 8


2. Using  notebook and select Kernel for .NET to run ONNX model

**Note**： Please download Microsoft Phi-3.5 ONNX model from Hugging face(https://huggingface.co/microsoft/Phi-3.5-mini-instruct-onnx) firstly



```bash

git lfs install

git clone https://huggingface.co/microsoft/Phi-3.5-mini-instruct-onnx

```

write this code in your notebook



```

#r "nuget: Microsoft.ML.OnnxRuntime, *-*"

#r "nuget: Microsoft.ML.OnnxRuntimeGenAI, *-*"

using Microsoft.ML.OnnxRuntimeGenAI;

string modelPath = @"Your Microsoft Phi-3.5 onnx model path"; 

var model = new Model(modelPath);

var tokenizer = new Tokenizer(model);

TokenizerStream tokenizerStream = tokenizer.CreateStream();

var input = "Can you introduce yourself?";

string prompt = "<|user|>" + input + "\n<|end|>\n<|assistant|>";

var sequences = tokenizer.Encode(prompt);

GeneratorParams gParams = new GeneratorParams(model);
gParams.SetSearchOption("max_length", 200);
gParams.SetInputSequences(sequences);
gParams.SetSearchOption("past_present_share_buffer", false);

Generator generator = new(model, gParams);

while (!generator.IsDone())
{
        generator.ComputeLogits();
        generator.GenerateNextToken();
        Console.Write(tokenizerStream.Decode(generator.GetSequence(0)[^1]));
}


```

**Note** Please focus that copy your onnx  dll to  onnxruntime genai folder








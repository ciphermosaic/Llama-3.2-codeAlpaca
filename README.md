# Llama-3.2-1B-Code-Instruct-GGUF

A lightweight coding assistant fine tuned from **Meta Llama 3.2 1B Instruct** on the **CodeAlpaca-20K** dataset. The model is optimized for instruction following in programming related tasks such as code generation, debugging, explaining code, and answering software development questions.

The model was fine tuned using **Unsloth** for efficient training and merged into a standalone checkpoint before being converted to **GGUF** for local inference with Ollama and llama.cpp compatible runtimes.

## Model Details

| Property              | Value                           |
| --------------------- | ------------------------------- |
| Model                 | Llama-3.2-1B-Code-Instruct-GGUF |
| Author                | ciphermosaic                    |
| Base Model            | Meta Llama-3.2-1B-Instruct      |
| Fine Tuning Framework | Unsloth                         |
| Dataset               | sahil2801/codeAlpaca-20k        |
| Quantization          | GGUF Q4_K_M                     |
| Intended Use          | Coding Assistant                |

## Training

The model was instruction tuned on the complete **CodeAlpaca-20K** dataset.

### Training Configuration

* Framework: Unsloth
* Precision: FP16
* 4-bit Loading: Enabled
* Per Device Batch Size: 2
* Gradient Accumulation Steps: 4
* Learning Rate: 2e-5
* Logging Steps: 25
* Save Strategy: Every Epoch

## Dataset

Training was performed using:

**Dataset:** `sahil2801/codeAlpaca-20k`

The dataset contains instruction and response pairs covering various programming tasks including:

* Code generation
* Code explanation
* Debugging
* Algorithm implementation
* Programming concepts
* Multiple programming languages

## Capabilities

The model performs well on tasks such as:

* Writing Python, C++, Java, JavaScript, and other programming languages
* Explaining existing code
* Debugging common programming errors
* Implementing algorithms and data structures
* Generating functions from natural language instructions
* Answering programming related questions

## Prompt Format

The model follows the Llama instruction format.

**Example**

```text
### Instruction:
Write a Python function to check if a string is a palindrome.

### Response:
```

## Running with Transformers

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

model_id = "ciphermosaic/Llama-3.2-1B-code-Instruct-GGUF"

tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(model_id)

prompt = "Write a Python function to reverse a linked list."

inputs = tokenizer(prompt, return_tensors="pt")

outputs = model.generate(**inputs, max_new_tokens=256)

print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```

## Running with Ollama

After downloading the GGUF model, create a Modelfile:

```text
FROM ./Llama-3.2-1B-Code-Instruct-Q4_K_M.gguf
```

Create the model:

```bash
ollama create llama32-code -f Modelfile
```

Run:

```bash
ollama run llama32-code
```





## Ollama Demo

![Ollama Demo](assets/Ollama_test.png)



## GGUF

This repository includes a GGUF version using:

* Q4_K_M

Compatible with:

* Ollama
* llama.cpp
* LM Studio
* Jan
* Open WebUI

## Limitations

* Designed primarily for coding related tasks.
* May generate incorrect or non optimal solutions for complex programming problems.
* Responses should be reviewed before use in production environments.
* Performance depends on prompt quality and task complexity.

## Intended Use

This model is intended for:

* Learning programming
* Code generation
* Debugging
* Software development assistance
* Educational use
* Local AI coding assistants

It is not intended for safety critical or production systems without human verification.

## Acknowledgements

* Meta AI for the Llama 3.2 base model.
* Unsloth for efficient fine tuning.
* Hugging Face for model hosting and ecosystem.
* sahil2801 for the CodeAlpaca-20K dataset.

## License

This model is derived from **Meta Llama 3.2** and is distributed under the **Llama 3.2 Community License**. Please ensure compliance with the original license terms when using or redistributing this model.

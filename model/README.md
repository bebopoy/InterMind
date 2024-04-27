---
pipeline_tag: text-generation
---
# InternLM 

<div align="center">

<img src="https://github.com/InternLM/InternLM/assets/22529082/b9788105-8892-4398-8b47-b513a292378e" width="200"/>
  <div>&nbsp;</div>
  <div align="center">
    <b><font size="5">InternLM</font></b>
    <sup>
      <a href="https://internlm.intern-ai.org.cn/">
        <i><font size="4">HOT</font></i>
      </a>
    </sup>
    <div>&nbsp;</div>
  </div>
  
[![evaluation](https://github.com/InternLM/InternLM/assets/22529082/f80a2a58-5ddf-471a-8da4-32ab65c8fd3b)](https://github.com/internLM/OpenCompass/)

[💻Github Repo](https://github.com/InternLM/InternLM) • [🤔Reporting Issues](https://github.com/InternLM/InternLM/issues/new)

</div>


## Introduction

InternLM2 has open-sourced a 7 billion parameter base model and a chat model tailored for practical scenarios. The model has the following characteristics:

- **200K Context window**: Nearly perfect at finding needles in the haystack with 200K-long context, with leading performance on long-context tasks like LongBench and L-Eval. Try it with [LMDeploy](https://github.com/InternLM/lmdeploy) for 200K-context inference.

- **Outstanding comprehensive performance**: Significantly better than the last generation in all dimensions, especially in reasoning, math, code, chat experience, instruction following, and creative writing, with leading performance among open-source models in similar sizes. In some evaluations, InternLM2-Chat-20B may match or even surpass ChatGPT (GPT-3.5).

- **Code interpreter & Data analysis**: With code interpreter, InternLM2-Chat-20B obtains compatible performance with GPT-4 on GSM8K and MATH. InternLM2-Chat also provides data analysis capability.

- **Stronger tool use**: Based on better tool utilization-related capabilities in instruction following, tool selection and reflection, InternLM2 can support more kinds of agents and multi-step tool calling for complex tasks. See [examples](https://github.com/InternLM/lagent).

## InternLM2-Chat-7B

### Performance Evaluation

We conducted a comprehensive evaluation of InternLM using the open-source evaluation tool [OpenCompass](https://github.com/internLM/OpenCompass/). The evaluation covered five dimensions of capabilities: disciplinary competence, language competence, knowledge competence, inference competence, and comprehension competence. Here are some of the evaluation results, and you can visit the [OpenCompass leaderboard](https://opencompass.org.cn/rank) for more evaluation results.

| Dataset\Models | InternLM2-7B | InternLM2-Chat-7B | InternLM2-20B | InternLM2-Chat-20B | ChatGPT | GPT-4 |
| --- | --- | --- | --- | --- | --- | --- |
| MMLU | 65.8 | 63.7 | 67.7 | 66.5 | 69.1 | 83.0 |
| AGIEval | 49.9 | 47.2 | 53.0 | 50.3 | 39.9 | 55.1 |
| BBH | 65.0 | 61.2 | 72.1 | 68.3 | 70.1 | 86.7 |
| GSM8K | 70.8 | 70.7 | 76.1 | 79.6 | 78.2 | 91.4 |
| MATH | 20.2 | 23.0 | 25.5 | 31.9 | 28.0 | 45.8 |
| HumanEval | 43.3 | 59.8 | 48.8 | 67.1 | 73.2 | 74.4 |
| MBPP(Sanitized) | 51.8 | 51.4 | 63.0 | 65.8 | 78.9 | 79.0 |

- The evaluation results were obtained from [OpenCompass](https://github.com/internLM/OpenCompass/) (some data marked with *, which means come from the original papers), and evaluation configuration can be found in the configuration files provided by [OpenCompass](https://github.com/internLM/OpenCompass/). 
- The evaluation data may have numerical differences due to the version iteration of [OpenCompass](https://github.com/internLM/OpenCompass/), so please refer to the latest evaluation results of [OpenCompass](https://github.com/internLM/OpenCompass/).


**Limitations:** Although we have made efforts to ensure the safety of the model during the training process and to encourage the model to generate text that complies with ethical and legal requirements, the model may still produce unexpected outputs due to its size and probabilistic generation paradigm. For example, the generated responses may contain biases, discrimination, or other harmful content. Please do not propagate such content. We are not responsible for any consequences resulting from the dissemination of harmful information.

### Import from ModelScope

To load the InternLM2 7B Chat model using ModelScope, use the following code:

```python
from modelscope import snapshot_download, AutoTokenizer, AutoModelForCausalLM
import torch

model_dir = snapshot_download("Shanghai_AI_Laboratory/internlm2-chat-7b")
tokenizer = AutoTokenizer.from_pretrained(model_dir, device_map="auto", trust_remote_code=True)
# Set `torch_dtype=torch.float16` to load model in float16, otherwise it will be loaded as float32 and might cause OOM Error.
model = AutoModelForCausalLM.from_pretrained(model_dir, device_map="auto",  trust_remote_code=True, torch_dtype=torch.float16)
model = model.eval()
response, history = model.chat(tokenizer, "hello", history=[])
print(response)
# Hello! How can I help you today?
response, history = model.chat(tokenizer, "please provide three suggestions about time management", history=history)
print(response)
```

The responses can be streamed using `stream_chat`:

```python
from modelscope import snapshot_download, AutoTokenizer, AutoModelForCausalLM
import torch

model_dir = snapshot_download("Shanghai_AI_Laboratory/internlm2-chat-7b")
tokenizer = AutoTokenizer.from_pretrained(model_dir, device_map="auto", trust_remote_code=True)
# Set `torch_dtype=torch.float16` to load model in float16, otherwise it will be loaded as float32 and might cause OOM Error.
model = AutoModelForCausalLM.from_pretrained(model_dir, device_map="auto",  trust_remote_code=True, torch_dtype=torch.float16)
model = model.eval()
length = 0
for response, history in model.stream_chat(tokenizer, "Hello", history=[]):
    print(response[length:], flush=True, end="")
    length = len(response)
```

## Open Source License

The code is licensed under Apache-2.0, while model weights are fully open for academic research and also allow **free** commercial usage. To apply for a commercial license, please fill in the [application form (English)](https://wj.qq.com/s2/12727483/5dba/)/[申请表（中文）](https://wj.qq.com/s2/12725412/f7c1/). For other questions or collaborations, please contact <internlm@pjlab.org.cn>.

## 简介

InternLM2 ，即书生·浦语大模型第二代，开源了面向实用场景的70亿参数基础模型与对话模型 （InternLM2-Chat-7B）。模型具有以下特点：

- 有效支持20万字超长上下文：模型在20万字长输入中几乎完美地实现长文“大海捞针”，而且在 LongBench 和 L-Eval 等长文任务中的表现也达到开源模型中的领先水平。 可以通过 [LMDeploy](https://github.com/InternLM/lmdeploy) 尝试20万字超长上下文推理。
- 综合性能全面提升：各能力维度相比上一代模型全面进步，在推理、数学、代码、对话体验、指令遵循和创意写作等方面的能力提升尤为显著，综合性能达到同量级开源模型的领先水平，在重点能力评测上 InternLM2-Chat-20B 能比肩甚至超越 ChatGPT （GPT-3.5）。
- 代码解释器与数据分析：在配合代码解释器（code-interpreter）的条件下，InternLM2-Chat-20B 在 GSM8K 和 MATH 上可以达到和 GPT-4 相仿的水平。基于在数理和工具方面强大的基础能力，InternLM2-Chat 提供了实用的数据分析能力。
- 工具调用能力整体升级：基于更强和更具有泛化性的指令理解、工具筛选与结果反思等能力，新版模型可以更可靠地支持复杂智能体的搭建，支持对工具进行有效的多轮调用，完成较复杂的任务。可以查看更多[样例](https://github.com/InternLM/lagent)。

## InternLM2-Chat-7B

### 性能评测

我们使用开源评测工具 [OpenCompass](https://github.com/internLM/OpenCompass/) 从学科综合能力、语言能力、知识能力、推理能力、理解能力五大能力维度对InternLM开展全面评测，部分评测结果如下表所示，欢迎访问[ OpenCompass 榜单 ](https://opencompass.org.cn/rank)获取更多的评测结果。

| 评测集 | InternLM2-7B | InternLM2-Chat-7B | InternLM2-20B | InternLM2-Chat-20B | ChatGPT | GPT-4 |
| --- | --- | --- | --- | --- | --- | --- |
| MMLU | 65.8 | 63.7 | 67.7 | 66.5 | 69.1 | 83.0 |
| AGIEval | 49.9 | 47.2 | 53.0 | 50.3 | 39.9 | 55.1 |
| BBH | 65.0 | 61.2 | 72.1 | 68.3 | 70.1 | 86.7 |
| GSM8K | 70.8 | 70.7 | 76.1 | 79.6 | 78.2 | 91.4 |
| MATH | 20.2 | 23.0 | 25.5 | 31.9 | 28.0 | 45.8 |
| HumanEval | 43.3 | 59.8 | 48.8 | 67.1 | 73.2 | 74.4 |
| MBPP(Sanitized) | 51.8 | 51.4 | 63.0 | 65.8 | 78.9 | 79.0 |

- 以上评测结果基于 [OpenCompass](https://github.com/internLM/OpenCompass/) 获得（部分数据标注`*`代表数据来自原始论文），具体测试细节可参见 [OpenCompass](https://github.com/internLM/OpenCompass/) 中提供的配置文件。
- 评测数据会因 [OpenCompass](https://github.com/internLM/OpenCompass/) 的版本迭代而存在数值差异，请以 [OpenCompass](https://github.com/internLM/OpenCompass/) 最新版的评测结果为主。

**局限性：** 尽管在训练过程中我们非常注重模型的安全性，尽力促使模型输出符合伦理和法律要求的文本，但受限于模型大小以及概率生成范式，模型可能会产生各种不符合预期的输出，例如回复内容包含偏见、歧视等有害内容，请勿传播这些内容。由于传播不良信息导致的任何后果，本项目不承担责任。

### 通过 ModelScope 加载

通过以下的代码加载 InternLM2 7B Chat 模型

```python
from modelscope import snapshot_download, AutoTokenizer, AutoModelForCausalLM
import torch

model_dir = snapshot_download("Shanghai_AI_Laboratory/internlm2-chat-7b")
tokenizer = AutoTokenizer.from_pretrained(model_dir, device_map="auto", trust_remote_code=True)
# `torch_dtype=torch.float16` 可以令模型以 float16 精度加载，否则 modelscope 会将模型加载为 float32，导致显存不足
model = AutoModelForCausalLM.from_pretrained(model_dir, device_map="auto",  trust_remote_code=True, torch_dtype=torch.float16)
model = model.eval()
response, history = model.chat(tokenizer, "你好", history=[])
print(response)
# 你好！有什么我可以帮助你的吗？
response, history = model.chat(tokenizer, "请提供三个管理时间的建议。", history=history)
print(response)
```

如果想进行流式生成，则可以使用 `stream_chat` 接口：

```python
from modelscope import snapshot_download, AutoTokenizer, AutoModelForCausalLM
import torch

model_dir = snapshot_download("Shanghai_AI_Laboratory/internlm2-chat-7b")
tokenizer = AutoTokenizer.from_pretrained(model_dir, device_map="auto", trust_remote_code=True)
# `torch_dtype=torch.float16` 可以令模型以 float16 精度加载，否则 modelscope 会将模型加载为 float32，导致显存不足
model = AutoModelForCausalLM.from_pretrained(model_dir, device_map="auto",  trust_remote_code=True, torch_dtype=torch.float16)
model = model.eval()
length = 0
for response, history in model.stream_chat(tokenizer, "你好", history=[]):
    print(response[length:], flush=True, end="")
    length = len(response)
```

## 开源许可证

本仓库的代码依照 Apache-2.0 协议开源。模型权重对学术研究完全开放，也可申请免费的商业使用授权（[申请表](https://wj.qq.com/s2/12725412/f7c1/)）。其他问题与合作请联系 <internlm@pjlab.org.cn>。
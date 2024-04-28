# InterMind assitant for mental health

InterMind is a mental health assistant that helps users manage their emotions and stress levels. It provides resources and support for individuals who are struggling with mental health issues.

InterMind是一款帮助用户管理情绪和压力水平的心理健康助手。它为那些与心理健康问题作斗争的个人提供资源和支持。

开源数据集来源[EmoLLM](https://github.com/SmartFlowAI/EmoLLM/tree/main/datasets)

项目贡献者 bebopoy、ACT-chao、leihuang

# 结构框架一览
```
├── config
│   └── internlm2_chat_7b_qlora_alpaca_e3_copy.py
├── data
│   ├── InterMind_data.jsonl
│   ├── convert_SoulStar_data.jsonl
│   └── convert_self_cognition_InterMind.jsonl
├── final_model
│   ├── config.json
│   ├── configuration_internlm2.py
│   ├── generation_config.json
│   ├── modeling_internlm2.py
│   ├── pytorch_model-00001-of-00008.bin
│   ├── pytorch_model-00002-of-00008.bin
│   ├── pytorch_model-00003-of-00008.bin
│   ├── pytorch_model-00004-of-00008.bin
│   ├── pytorch_model-00005-of-00008.bin
│   ├── pytorch_model-00006-of-00008.bin
│   ├── pytorch_model-00007-of-00008.bin
│   ├── pytorch_model-00008-of-00008.bin
│   ├── pytorch_model.bin.index.json
│   ├── special_tokens_map.json
│   ├── tokenization_internlm2.py
│   ├── tokenization_internlm2_fast.py
│   ├── tokenizer.json
│   ├── tokenizer.model
│   └── tokenizer_config.json
├── huggingface
│   ├── README.md
│   ├── adapter_config.json
│   ├── adapter_model.bin
│   └── xtuner_config.py
├── model
│   ├── README.md
│   ├── config.json
│   ├── configuration.json
│   ├── configuration_internlm2.py
│   ├── generation_config.json
│   ├── model-00001-of-00008.safetensors
│   ├── model-00002-of-00008.safetensors
│   ├── model-00003-of-00008.safetensors
│   ├── model-00004-of-00008.safetensors
│   ├── model-00005-of-00008.safetensors
│   ├── model-00006-of-00008.safetensors
│   ├── model-00007-of-00008.safetensors
│   ├── model-00008-of-00008.safetensors
│   ├── model.safetensors.index.json
│   ├── modeling_internlm2.py
│   ├── special_tokens_map.json
│   ├── tokenization_internlm2.py
│   ├── tokenization_internlm2_fast.py
│   ├── tokenizer.model
│   └── tokenizer_config.json
├── requirements.txt
├── train
│   ├── 20240426_225819
│   │   ├── 20240426_225819.log
│   │   └── vis_data
│   │       └── config.py
│   ├── 20240426_231034
│   │   └── vis_data
│   │       ├── 20240426_231034.json
│   │       ├── config.py
│   │       ├── eval_outputs_iter_1499.txt
│   │       ├── eval_outputs
```
# model-基于InternLM2_chat_7b

存放初始模型文件,详情请见[InternLM2-Chat-7B](https://github.com/bebopoy/InterMind/blob/master/model/README.md)说明文档
# config 

存放了配置文件——internlm2_chat_7b_qlora_alpaca_e3_copy.py用于对模型进行微调，可[参考说明](https://github.com/InternLM/xtuner/blob/main/docs/zh_cn/user_guides/config.md)
# data 
存放数据集——InterMind_data.jsonl，包含了单轮次对话数据集与自我认知数据集。
单轮次对话数据集——*convert_SoulStar_data.jsonl*（数据来源[EmoLLM](https://github.com/SmartFlowAI/EmoLLM/tree/main/datasets)）
自我认知数据集——*convert_self_cognition_InterMind.jsonl*
# train
存放训练所得.pth 文件，有iter_7500.th和iter_8000.th,分别为7000轮次和8000轮此的训练结果，以待被转化为hunggingface文件（Adapter）
# hunggingface
存放hunggingface文件（Adapter）,以待被合并为大预言模型并送至final_model文件中
# final_model 
存放了训练成果的模型——InterMind 聊天机器人
#   web_demo
存放了web_demo文件，用于web演示
#   requirments.txt
python第三方库环境要求

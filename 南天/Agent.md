

![[Pasted image 20240830101926.png]]



# OpenAI
![[Pasted image 20240830104249.png]]





# 框架

- Qwen-Agent
- AutoGen
- CrawAI



# 多Agent
CrawAI



#  AutoGent





# 部署


```
python -m vllm.entrypoints.openai.api_server \
--model /home/niwang/models/Qwen2-7B-Instruct \
--max-model-len 8192
```


# 数据

MSAgent-Bench
## 1. ToolBench

ToolBench 是一个广泛使用的英文数据集，专注于工具学习能力的评估。它为模型提供了多种工具调用的示例，但主要是英文数据，这可能在中文环境中存在一定的局限性[](https://blog.csdn.net/CodeFuse/article/details/135508949)。

## 2. ToolLearning-Eval

CodeFuse 发布了首个中文的评测基准 ToolLearning-Eval，旨在评估大语言模型在工具学习领域的表现。该数据集包括239种工具类别，涵盖59个领域，共有1509条评测数据。数据来源包括开源数据、翻译的ToolBench数据和使用Self-Instruct方法生成的中文数据[](https://blog.csdn.net/CodeFuse/article/details/135508949)。



# 模型部署




```bash



nohup python -m vllm.entrypoints.openai.api_server \
    --model /home/niwang/code/nantian-llm-demo/output/qwen2-1_5b-instruct/v7-20240815-111824/checkpoint-30 \
    --port 6006 \
    --max-model-len 2048 \
    --trust-remote-code
    &
```





# 提示词


```
尽你所能回答以下问题。你拥有如下工具：

{'name': 'get_current_weather', 'description': 'Get the current weather in a given location', 'parameters': {'type': 'object', 'properties': {'location': {'type': 'string', 'description': 'The city and state, e.g. San Francisco, CA'}, 'unit': {'type': 'string', 'enum': ['celsius', 'fahrenheit']}}, 'required': ['location']}}

以下格式回答：

Thought: 思考你应该做什么
Action: 工具的名称，必须是[get_current_weather]之一
Action Input: 工具的输入

开始！

问题：你能帮我生成一张小狗的画吗？
```



# VL 模型



```

qwen-vl-plus

sk-4abd28915baa44f98b860fcc36003da3


https://help.aliyun.com/zh/model-studio/developer-reference/qwen-vl-api?spm=a2c4g.11186623.0.i2#6c780db866i8l
```
### **LLM**

大语言模型，简称大模型

基于 Transformer 架构（Google），后续会讲到

GPT 系列 大模型浪潮的鼻祖

**大模型工作原理：**

1. 迭代式生成：模型在每一步都基于已有的文本序列，预测下一个最可能的词（或子词，即token）
2. 自回归：每次生成的词会被追加到输入序列中，作为下一步生成的新上下文
3. 停止条件：这个过程持续进行，直到模型生成一个特殊的“结束符”或达到设定的最大长度限制



### Token

大模型里进行的其实是庞大的矩阵运算，输入和输出都是数字

那么，我们输入的文字如何转换成数字交付给大模型？

Tokenizer 桥梁 进行编码和解码

编码：切分+映射，把输入的文字切分成一个个token，然后分别映射成数字（token ID），交付给大模型

解码：映射，数字映射回文字，给到用户

**token 是大模型处理文本的最基本单位**

token 和 词 不完全等同，一个 token 不一定刚好是一个词

openai 提供了一个工具来计算文本的 token：https://platform.openai.com/tokenizer

可以尝试一下，比如“程序员”这个词就对应两个token

1 token ≈ 1.5 个汉字



### Context

**context 是上下文，代表模型每次处理任务时所接收到的信息总和**

**包括对话历史、用户问题、当前输出的 token （被追加进 context 中）、工具列表、system prompt 等**

context window 上下文窗口，代表 context 能容纳的最大 token 数

目前主流的一些大模型，比如 GPT 的上下问窗口就是 105 万，其他也都在 100 万左右

如果知识库太大，不适合整个发给大模型，可以采用 RAG 技术，只检索其中最匹配的几个片段发给大模型



### Prompt

**prompt 就是提示词**，给大模型的指令

prompt engineering 提示词工程，专门研究怎么把提示词说得更明白，让大模型更清晰的理解你的意图，从而提高回答的质量

（现在这个领域已经不是那么热门了，随着大模型能力增强，即使提示词含糊不清也能大致理解意图）

prompt 可以分为两类：

1. **user prompt 用户提示词**，即用户的输入，描述具体任务
2. **system prompt 系统提示词**，即即后台给大模型配置的人设和具体做事规则



### Tools

工具，类似一个函数，有输入输出

**给大模型提供它可以调用的外部能力，让大模型能感知和影响外部环境**

![image-20260323012043499](C:\Users\Emma\AppData\Roaming\Typora\typora-user-images\image-20260323012043499.png)



### MCP

在以上过程中，可以看到平台需要告诉大模型有哪些工具，还要调用工具，所以我们需要先把工具接入平台里

不同平台的接入标准不同，每换一个平台，就需要重新写一套接入规范

**MCP 统一了工具接入格式的标准协议**（Model Context Protool 模型上下文协议）



### Agent

**Agent 能自主规划和调用工具，直至解决用户问题的程序**

![image-20260323013237563](C:\Users\Emma\AppData\Roaming\Typora\typora-user-images\image-20260323013237563.png)

流行的 Agent 有 Claude Code，Codex，Gemini CLI等，构建模型有 React，Plan And Execute



### Agent Skills

**给 Agent 看的说明文档**

元数据层（name + description）+ 指令层

![image-20260323021425708](C:\Users\Emma\AppData\Roaming\Typora\typora-user-images\image-20260323021425708.png)
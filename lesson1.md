# InternLM第一课笔记-书生·浦语大模型全链路开源体系

# 全链条工具体系

> 提供数据集->预训练->微调->部署->评测->应用全套工具。

数据：书生万卷 https://opendatalab.org.cn/

预训练：InternLM-Train -只需修改配置文件，即可实现不同模型、不同数据集下的训练。

微调：XTuner - 内置Lora、QLora等多种微调算法

- 支持加载开源数据集：HuggingFace，ModelScope
- 最低只需8GB显存即可支持7B模型 部署：LMDeploy

部署：LMDeploy -支持高效部署，内置INT4、INT8量化实现

- 接口：Python,gRPC,RESTful
- 轻量化：4bit权重，8bit k/v
- 推理引擎：turbomind,pytorch (支持交互式，或非交互式的推理）
- 服务：openai-server，gradio,trition inference server

评测：OpenCompass

- CompassRank:大语言模型榜单，多模态模型榜单
- CompassKit：数据污染检查（GSM-8K,MMLU等主流数据集的污染监测），模型推理接入，长文本能力评测，中英文双语主观评测
- CompassHub 高质量测评计准社区

应用：Lagent [GitHub - InternLM/lagent: A lightweight framework for building LLM-based agents](https://github.com/InternLM/lagent)

- 智能体构建工具包，构建智能体查询外部资料如网站、文档等，提高模型回答准确性与可靠性。同时支持图像、文字、语音等多种模态。
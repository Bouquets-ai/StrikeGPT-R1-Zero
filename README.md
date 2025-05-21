# 🤖 StrikeGPT-R1-Zero: 网络安全渗透领域推理模型 

<img width="451" alt="image" src="https://github.com/user-attachments/assets/de75af40-3b9a-4e7b-80e4-c934175bbfb9" />


## 🚀 模型简介  
**StrikeGPT-R1-Zero** 是基于 **Qwen3** 进行黑盒蒸馏的专家模型，其教师模型为 DeepSeek-R1，涵盖：  
🔒 AI安全 | 🛡️ API安全 | 📱 APP安全 | 🕵️ APT | 🚩 CTF  
🏭 ICS安全 | 💻 渗透测试ALL | ☁️ 云上安全 | 📜 代码审计  
🦠 免杀 | 🌐 内网安全 | 💾 电子取证 | ₿ 区块链安全 | 🕳️ 溯源反制 | 🌍 物联网(IoT)安全<br>
🚨 应急响应 | 🚗 整车安全 | 👥 社会工程学 | 💼 渗透测试面试 
### 👉 [点击访问可交互式详细数据分布图](https://bouquets-ai.github.io/StrikeGPT-R1-Zero/WEB)  
### 🌟 模型亮点
- 🧩采用**思维链(CoT)推理数据**优化模型逻辑能力，显著提升在漏洞分析等复杂任务的表现
- 💪Base模型采用Qwen3相较于Distill-Llama更适合中国宝宝体制
- ⚠️**无道德限制**在特定领域的学术研究有不一样的表现（请在符合当地法律的情况下使用）
- ✨特定情况下如断网状态下的**网络安全大赛**，相较于本地RAG形式StrikeGPT-R1-Zero逻辑推理能力更强，在复杂任务处理方面表现更佳。
   
## 📊 数据分布  
![data](https://github.com/user-attachments/assets/4d19d48d-67bb-4b05-8ce9-2000b6afa12e)


## 🛠️模型部署
### 通过ollama进行部署
`ollama run hf.co/Bouquets/StrikeGPT-R1-Zero-8B-Q4_K_M-GGUF:Q4_K_M`

**也可以直接调用原始模型**
```
from unsloth import FastLanguageModel
import torch
max_seq_length = 2048 # Choose any! We auto support RoPE Scaling internally!
dtype = None # None for auto detection. Float16 for Tesla T4, V100, Bfloat16 for Ampere+
load_in_4bit = True # Use 4bit quantization to reduce memory usage. Can be False.


model, tokenizer = FastLanguageModel.from_pretrained(
    model_name = "Bouquets/StrikeGPT-R1-Zero-8B",
    max_seq_length = max_seq_length,
    dtype = dtype,
    load_in_4bit = load_in_4bit,
    # token = "hf_...",
)
alpaca_prompt = """Below is an instruction that describes a task, paired with an input that provides further context. Write a response that appropriately completes the request.

### Instruction:
{}

### Input:
{}

### Response:
{}"""
# alpaca_prompt = Copied from above
FastLanguageModel.for_inference(model) # Enable native 2x faster inference
inputs = tokenizer(
[
    alpaca_prompt.format(
        "", # instruction
        "你好，你是openai开发的吗", # input
        "", # output - leave this blank for generation!
    )
], return_tensors = "pt").to("cuda")

from transformers import TextStreamer
text_streamer = TextStreamer(tokenizer, skip_prompt = True)
_ = model.generate(input_ids = inputs.input_ids, attention_mask = inputs.attention_mask,
                   streamer = text_streamer, max_new_tokens = 4096, pad_token_id = tokenizer.eos_token_id)
```
![image](https://github.com/user-attachments/assets/d8cef659-3c83-4bc9-af1a-78ed6345faf2)

经过量化后自我认知有点问题,请不要在意
![image](https://github.com/user-attachments/assets/3989ea09-d581-49fb-9938-01b93e0beb91)
## 💻开源💻
🌟 **开源模型** 🌟  
🤗 **HuggingFace**:  
🔗 [https://huggingface.co/Bouquets/StrikeGPT-R1-Zero-8B](https://huggingface.co/Bouquets/StrikeGPT-R1-Zero-8B)  

📊 **数据集** (部分非推理数据集) 📊  
🤗 **HuggingFace**:  
🔹 网络安全LLM-CVE数据集:  
🔗 [https://huggingface.co/datasets/Bouquets/Cybersecurity-LLM-CVE](https://huggingface.co/datasets/Bouquets/Cybersecurity-LLM-CVE)  

🔹 红队LLM英文数据集:  
🔗 [https://huggingface.co/datasets/Bouquets/Cybersecurity-Red_team-LLM-en](https://huggingface.co/datasets/Bouquets/Cybersecurity-Red_team-LLM-en) 



## 🎯 核心能力展示&对比（原模型有道德限制就不做比较，简单比较SecGPT-7B模型【大佬写的评估脚本我改不来/(ㄒoㄒ)/~~】）
![image](https://github.com/user-attachments/assets/8166a1d3-c69f-4b8a-821f-0dd83dcd4544)

### CTF
![image](https://github.com/user-attachments/assets/e6552b0b-521f-4d3f-8ba1-b9a3ce136d65)
![image](https://github.com/user-attachments/assets/df55e964-0bc3-45a9-97a6-625ea9d086fe)

#### Reverse Engineering
![image](https://github.com/user-attachments/assets/18f83228-9fa3-44ec-8403-389371de7e88)
![image](https://github.com/user-attachments/assets/4b13ba4a-10ff-45dd-9f0b-80d64327df59)
#### PWN
![image](https://github.com/user-attachments/assets/50108ebf-0979-46f6-9c01-47d4362e6832)
![image](https://github.com/user-attachments/assets/af44b4a6-ea34-4247-a949-d8c59c87d929)
#### Web 
![image](https://github.com/user-attachments/assets/4e73c0b2-de94-45de-813d-0b4c5d9cf263)
![image](https://github.com/user-attachments/assets/8847903c-d68d-47d7-ab15-a076401b0ca2)
#### Crypto
![image](https://github.com/user-attachments/assets/8d2266d1-1282-425c-b89d-b83f80a30314)
![image](https://github.com/user-attachments/assets/991b84f5-600b-4646-aac5-2b1c4d1712c1)

#### Misc
![image](https://github.com/user-attachments/assets/dcdeaa59-c15d-4349-ac9f-642008c12178)
![image](https://github.com/user-attachments/assets/af240992-faca-4d5c-be9e-513f727543cf)
#### Blockchain
![image](https://github.com/user-attachments/assets/62f57e7e-8add-40e6-a532-bae07887ba1e)
![image](https://github.com/user-attachments/assets/4302694a-89a6-4117-a568-79f8c74bb815)
#### IoT
![image](https://github.com/user-attachments/assets/d30a620f-f5e7-473c-a2f5-2ae171479e3f)
![image](https://github.com/user-attachments/assets/bb3288b4-fa47-4265-9a30-8fdd62b1e651)

### 内网安全
![image](https://github.com/user-attachments/assets/02fba088-9419-47ec-9072-de9a362a4e08)
![image](https://github.com/user-attachments/assets/05e9aef3-690f-4608-998c-8715e1a90e59)

### 社工
![image](https://github.com/user-attachments/assets/6e1eb9ec-1bf5-4bc2-acdf-c5b004b58f6e)
![image](https://github.com/user-attachments/assets/f0c93222-56e6-4253-b6bb-3eeb8ec7d9cf)

### 代码编写
![image](https://github.com/user-attachments/assets/6e037fff-e46b-42d5-997d-559fb300aba0)
![image](https://github.com/user-attachments/assets/e8c1c0fd-16af-46e1-8b7b-57947145f545)

### 代码审计（联动项目DeepSeekSelfTool）
![image](https://github.com/user-attachments/assets/c7dc4b66-379d-4c57-aaf2-3d4d73d1484c)
![image](https://github.com/user-attachments/assets/69a692a5-3290-4062-a4c7-de34c22d4d90)
![image](https://github.com/user-attachments/assets/b3df6f14-ccf0-44ec-ac69-c673ed1398c6)



## 📈 实验数据走势图 
有些许梯度爆炸，总体问题不大
![image](https://github.com/user-attachments/assets/a3fa3676-9f07-47ea-9029-ec0d56fdc989)

## 💰 训练成本  
- **DeepSeek-R1 API调用费用**: ¥450 (均在打折时调用，正常调用价格在¥1800)
- **服务器开销**: ¥4?0
- **电子资源**: ¥??
  ![image](https://github.com/user-attachments/assets/8e23b5b6-24d9-47c3-b54f-ffa22ec68a83)


## ⚖️ 使用须知 
> 本模型仅供**合法安全研究**与**教育用途**。使用者需遵守所在地法律法规，开发者不对滥用行为负责。<br>
> 提示：使用即表示您同意本声明

💡 **提示**: 模型可能存在幻觉或知识盲区，关键场景请交叉验证！  


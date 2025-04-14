
# ⚠It's still being tested,Only the Chinese dataset was used⚠ 

# Distillation data distribution
![](https://github.com/Bouquets-ai/StrikeGPT-R1-Zero/blob/main/img/data.gif)
![](https://github.com/Bouquets-ai/StrikeGPT-R1-Zero/blob/main/img/%25E5%25BE%25AE%25E4%25BF%25A1%25E6%2588%25AA%25E5%259B%25BE_20250409152539.png?raw=true)
![](https://github.com/Bouquets-ai/StrikeGPT-R1-Zero/blob/main/img/%25E5%25BE%25AE%25E4%25BF%25A1%25E6%2588%25AA%25E5%259B%25BE_20250409152742.png?raw=true)

# 思考
1.目前只使用蒸馏模型对Deepseek-R1进行二次蒸馏，其实按照技术流程，这是完全可行的，只不过推理能力相较于GRPO略微逊色一些

2.尝试过GRPO+SFT因奖励问题难以达到心里预期，感觉在安全领域标准答案定义太模糊了，日志流量分析类和代码审计类有固定答案类目前看来较为适用，纯渗透领域还是太难了。

3.尝试过logits蒸馏+KL散度或者交叉熵，目前看来前向KL散度为最优解，也可以试试反向和偏前偏反，苦于博主学校不支援GPU未能使用较好的教师模型，也因博主技术原因造成了欠拟合和梯度爆炸，不过进行加权和控制梯度也能暂时缓解，一来二去模型成傻子了，哎。

4.哎，今年要准备别的事希望有好消息，明年准备从零手搓一个专注于渗透的推理安全大模型，从技术来说知识储备问题已经不大了，就差时间和GPU还有超高质量的数据（废话）。再多多想着如何能与MCP结合一下，暂时专注于简单的CTF和安服类脚本小子的替代工作。

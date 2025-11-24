---
timezone: UTC+8
---

# 黄文晔

**GitHub ID:** Eeeeye

**Telegram:** @Eeeeye

## Self-introduction

大三

## Notes

<!-- Content_START -->
# 2025-11-24
<!-- DAILY_CHECKIN_2025-11-24_START -->
## **Task1**

```
 npm install -g zetachain         
zetachain query chains list
```

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-24-1764000144501-image.png)

## **Task2**

![截图 2025-11-24 23-39-08.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-24-1764000078427-___2025-11-24_23-39-08.png)

generate the API key and use python visual environment to run [test.sh](http://test.sh)

here is the content of .sh(the "DASHSCOPE\_API\_KEY" has been set to my API\_KEY:

```
import os
from openai import OpenAI
​
client = OpenAI(
    # 若没有配置环境变量，请用百炼API Key将下行替换为：api_key="sk-xxx",
    api_key=os.getenv("DASHSCOPE_API_KEY"),
    base_url="https://dashscope.aliyuncs.com/compatible-mode/v1",
)
completion = client.chat.completions.create(
    model="qwen3-max",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "你是谁？"},
    ],
    stream=True
)
for chunk in completion:
    print(chunk.choices[0].delta.content, end="", flush=True)
```

![截图 2025-11-24 23-53-41.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-24-1764000048047-___2025-11-24_23-53-41.png)

## **Task3**

Join the community in wechat

![image.png](https://raw.githubusercontent.com/IntensiveCoLearning/Universal-AI/main/assets/Eeeeye/images/2025-11-24-1764000110205-image.png)
<!-- DAILY_CHECKIN_2025-11-24_END -->
<!-- Content_END -->

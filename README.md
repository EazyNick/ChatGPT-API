# ChatGPT API 사용법

OpenAI의 ChatGPT API를 사용하는 방법 / 24.08 기준
현재 main.ipynb에서는 기아차 주가를 불러와서, 주가를 바탕으로 gpt에게 매수하면 좋을지, 매도하면 좋을지를 점수로 알려달라는 질문을 하고있습니다.<br>
실제 API 요청 부분은 아래 코드를 참고해주세요.
<br>

<br>

```python
from openai import OpenAI

# 본인의 API 키 작성
client = OpenAI(api_key='Your-Key')

GPT_MODEL = "gpt-3.5-turbo" #"gpt-3.5-turbo-1106"
# 프롬프트 구성
messages = [
    {"role": "system", "content": "You are a financial assistant specialized in stock market predictions."},
    {"role": "user", "content": f"Here is the historical weekly stock data for Kia Motors for the past month including the 5-day Simple Moving Average (SMA):\n\n{data_str}\n\nBased on this data, predict the stock's future performance and provide a score between -1000 (sell) and 1000 (buy). Only return the score as a number without any additional text."}
]
response = client.chat_completions.create(
        model=GPT_MODEL,
        messages=messages,
        temperature=0
    )
response_message = response.choices[0].message['content']
print(f"response_message: {response_message}")
```

## 요구 사항

- Python 3.6 이상
- OpenAI API 키

## 설치

필요한 라이브러리를 설치합니다:

```bash
pip install openai

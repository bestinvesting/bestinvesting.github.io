---
title: 📊 볼린저밴드스퀴즈 CODE
author: best investor
date: 2025-03-11
category: Jekyll
layout: post
---




---

비트코인 데이터에 대해 **볼린저 스퀴즈 전략**을 적용하고, 성과를 분석 

---

✅ **기능:**  
- 볼린저 밴드(20, 2) 계산  
- 스퀴즈 발생 탐지 (밴드 폭이 일정 임계값 이하)  
- 가격이 상단/하단 돌파 시 매매  
- 성과 분석 (수익률, 승률, 최대 손실 등)  

---

🔹 **코드 실행 순서**  
1. 비트코인 데이터 다운로드 (yfinance 사용)  
2. 볼린저 밴드 계산  
3. 스퀴즈 발생 확인 및 진입 조건 설정  
4. 전략 백테스트  
5. 성과 분석 및 시각화  

---

**📌 Python 코드**
```
import pandas as pd
import numpy as np
import yfinance as yf
import matplotlib.pyplot as plt

# 1️⃣ 비트코인 데이터 다운로드
symbol = "BTC-USD"
data = yf.download(symbol, start="2022-01-01", end="2025-01-01")

# 2️⃣ 볼린저 밴드 계산 (20일 이동평균 + 표준편차)
window = 20
std_dev = 2
data['SMA'] = data['Close'].rolling(window).mean()
data['STD'] = data['Close'].rolling(window).std()
data['Upper'] = data['SMA'] + (data['STD'] * std_dev)
data['Lower'] = data['SMA'] - (data['STD'] * std_dev)
data['Band_Width'] = data['Upper'] - data['Lower']

# 3️⃣ 스퀴즈 발생 탐지 (밴드 폭이 일정 임계값 이하)
squeeze_threshold = data['Band_Width'].rolling(window).mean() * 0.8
data['Squeeze'] = data['Band_Width'] < squeeze_threshold

# 4️⃣ 매매 신호 생성 (스퀴즈 후 돌파 여부 확인)
data['Long_Entry'] = (data['Squeeze']) & (data['Close'] > data['Upper'])
data['Short_Entry'] = (data['Squeeze']) & (data['Close'] < data['Lower'])

data['Position'] = 0
data.loc[data['Long_Entry'], 'Position'] = 1  # 롱 포지션
\data.loc[data['Short_Entry'], 'Position'] = -1  # 숏 포지션

data['Position'] = data['Position'].shift(1).fillna(0)  # 신호 다음날 진입

# 5️⃣ 백테스트: 일별 수익률 계산
data['Returns'] = data['Close'].pct_change()
data['Strategy'] = data['Position'].shift(1) * data['Returns']

cumulative_strategy = (1 + data['Strategy']).cumprod()
cumulative_market = (1 + data['Returns']).cumprod()

# 6️⃣ 성과 지표 계산
final_return = cumulative_strategy.iloc[-1] - 1
win_rate = (data['Strategy'] > 0).sum() / (data['Strategy'] != 0).sum()
max_drawdown = (cumulative_strategy / cumulative_strategy.cummax() - 1).min()

print(f"📈 최종 수익률: {final_return:.2%}")
print(f"✅ 승률: {win_rate:.2%}")
print(f"⚠️ 최대 손실(Drawdown): {max_drawdown:.2%}")

# 7️⃣ 성과 시각화
plt.figure(figsize=(12, 6))
plt.plot(cumulative_strategy, label='Bollinger Squeeze Strategy', color='blue')
plt.plot(cumulative_market, label='Market (BTC)', color='gray', linestyle='dashed')
plt.legend()
plt.title('Bollinger Squeeze Strategy Performance')
plt.xlabel('Date')
plt.ylabel('Cumulative Returns')
plt.show()
```

📊 **결과 분석**  
- **최종 수익률:** 백테스트 기간 동안의 전략 성과  
- **승률:** 롱/숏 진입 시 성공한 비율  
- **최대 손실:** 전략의 최대 하락폭 (Drawdown)  
- **시각화:** 전략 수익률 vs. 시장 수익률 비교  



---
layout: post
title: ChatGPT APIで多言語Twitterボットを作ってみた話
postHero: /images/code-hero.jpg
author: Kyogo Sato
authorTwitter: https://twitter.com/kyogosato
gravatar: https://gravatar.com/avatar/ffda7d145b83c4b118f982401f962ca6?s=150
postFooter: 実験と失敗の繰り返しが、いちばんの勉強法。<a href="#">#AI #Python</a>
---

最近、OpenAIのChatGPT APIを使って**10か国語対応の筋トレBot**を作ってみました。  
日本語で投稿した内容を、各国語に自動翻訳してツイートする仕組みです。  
この記事では、その中で特に苦戦した「翻訳部分のチューニング」について紹介します。

---

## 1. 最初の設計：単純な翻訳では不自然だった

最初は、シンプルにChatGPT APIを呼び出すだけでした。

```python
translated = openai.ChatCompletion.create(
  model="gpt-4o-mini",
  messages=[
    {"role": "system", "content": "Translate into Spanish."},
    {"role": "user", "content": original_text}
  ]
)

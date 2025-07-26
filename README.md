# Line-English-Bot
LINE English Vocabulary Bot with FAISS and GPT
# LINE 英文單字查詢機器人

這是一個使用 Flask + FAISS 向量搜尋 + OpenAI GPT 的 LINE 聊天機器人範例，  
能辨識用戶輸入是英文單字或句子，並根據條件使用向量比對或 GPT 回答。

---

## 功能說明

- 用戶輸入 **英文單字** 時，使用 FAISS 進行向量相似度比對，提供對應中文解釋。  
- 當在向量庫中找不到此英文單字時, 直接使用GPT產生回答
- 用戶輸入 **非英文單字** 或 **英文句子** 時，直接使用 GPT 產生回答。  
- 結合 LINE Messaging API，可透過 LINE 與機器人互動。

---

## 使用方法

1. 先準備 OpenAI API Key，設定環境變數 `OPENAI_API_KEY`  
2. 下載並上傳多益單字檔案（格式：英文單字與中文解釋交錯排列）  
3. 設定 LINE Bot 的 Channel Access Token 與 Channel Secret（環境變數 `LINE_CHANNEL_ACCESS_TOKEN`, `LINE_CHANNEL_SECRET`）  
4. 執行 `app.py`，啟動服務，並將 ngrok 產生的公開網址設定為 LINE Webhook
5. 透過 LINE 聊天即可開始互動

---

## 主要程式碼結構說明

- `query_gpt_fallback(q)`  
  使用 OpenAI ChatCompletion API 回傳 GPT 回答。  

- `is_english_word(text)`  
  判斷是否為純英文單字（只包含英文字母）。  

- `is_english_sentence(text)`  
  判斷是否為英文句子（包含標點符號及空白，詞數大於1）。  

- `/query` 路由  
  判斷用戶輸入，決定使用 FAISS 向量搜尋或 GPT 回應。  

- Line Bot 事件處理  
  接收訊息並回覆，結合 LINE Messaging API。

---

## 依賴套件

- flask
- pyngrok
- sentence-transformers
- faiss-cpu
- openai==0.28
- line-bot-sdk

---

## 注意事項

- 請確保你的環境有設定好所有必須的環境變數。  
- 多益單字檔格式需為交錯的英文、中文兩行一組。  
- ngrok 用來建立本地服務的公開網址，須確保 ngrok 可用。

---

## 授權

MIT License


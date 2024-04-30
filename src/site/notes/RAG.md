---
{"dg-publish":true,"permalink":"/rag/"}
---



```ad-summary
title: RAG 是什麼？

**R**etrieval-**A**gumented **G**eneration

**RAG** 是一種調整推論(Inference)結果為目標的方法。
```



# RAG Pipeline
![RAG Process](https://miro.medium.com/v2/resize:fit:720/format:webp/1*33zN9mJugzjcSEcV-PAhig.gif)

使用者會藉由聊天機器人 (Chatbot) 詢問問題，Chatbot 在讀取人類輸入的問題後，會*搜尋知識庫*中的文件內容，並*結合提示工程* 來提供大語言模型 (LLM) 理解並回傳給使用者做為使用者問題的回應。

Python 中要完成 RAG 的主流框架目前有兩種：
1. **LlamaIndex**：專門使用**內容增強 (Context-Augmented)** 來調整 LLM 輸出的框架。
2. **Langchain**：**整合 LLM 中流程與工具**的框架，可以說是瑞士刀一般的存在。

RAG 中會使用 LlamaIndex **建構並檢索知識庫**，並在後續的**提示工程**與 LLM 讀取等使用 Langchain 整合為問題的回答。



# 搜尋知識庫 
RAG 過程中是 *如何搜尋知識庫的？* 我們可以從 [LlamaIndex 中提及 RAG 執行流程](https://docs.llamaindex.ai/en/stable/getting_started/concepts/#important-concepts-within-each-step)的幾個步驟來說明：
1. **Loading** stage (讀取與整理知識庫文件)
2. **Indexing** stage (建立知識庫索引)
3. **Querying** stage (檢索知識庫)

知識庫本身技術是**向量資料庫**的建立，主要目的是數值化文句中的語意，並以方便查找的方式存取下來。而數值化的結果是以多個維度的矩陣組成，稱之為向量。建立資料庫以方便查找，儲存並管理向量的資料庫則是向量資料庫。

**數值化文句語意會交給機器學習模型來轉換**，由於 Rule base 無法窮舉所有文句的語意，所以採用機器學習演算法來為語意的表達找出規則。找出的規則一般會稱為模型，而 RAG 中專門數值化語意的模型則稱為 **Embedding Model**。

## Loading 讀取與整理知識庫文件 
讀取的文件，依據資料**是否為資料表**的面向，分為兩種類型：
1. **結構化資料**：即是可以成為資料表的資料。
2. **非結構化資料**：即是無法成為資料表的資料。

**非結構化資料**是 **LLM** 擅長的項目，但是**結構化資料**又能夠提供**檢索知識庫**上的幫助。所以為了使 LLM 能夠發揮功能，又要讓檢索能夠快速定位。

一般情況，基本上是以結構化資料中含有非結構化資料的資料，最為容易進行下一步的向量資料庫建立。


## Indexing 建立知識庫索引


## Querying 檢索知識庫



# 結合提示工程
提示工程全名為 **Prompt Engineering**，是一種限定 LLM 輸出範圍的方式。隨著不同的 Prompt 能夠給予大語言模型不同的角色，控制大語言模型能夠回答出更貼近使用者所期望的領域內容。

Prompt Engineering 是作用於模型文字的生成階段，是由**系統中進行定義**而非由使用者來提供。Prompt Enigneering 會在系統內部賦予大語言模型一個符合需求的角色，並整合搜尋到的文件作為大語言模型的問題。大語言模型則會**理解輸入的文字**，並進一步轉換為可供人類閱讀的語句來作為回應。

若是純粹僅僅要靠著不調整 (Fine-tune) 模型，提示工程更是重要。但是提示工程無法準確評估可能的輸出或是調整上是無法有一套有規劃的邏輯，所以可以藉由**自動化方式評估提示詞的效果**來加速提示工程的進度，能夠快速收斂結果。

> 自動化提示工程：[[gpt-prompt-engineer 使用心得\|gpt-prompt-engineer 使用心得]]

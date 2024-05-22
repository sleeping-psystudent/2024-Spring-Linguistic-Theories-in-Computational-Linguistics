# 作業二：LangChain
## Part 1: Building a Simple QA App

🔺請依照以下指示，創建 1 個 LLMchain，並用其回答指定問題：

1. **Install and import necessary libraries**
2. **Define an LLM** <5分>
  - 定義一個你想使用的模型
  - Either an LLM model or a Chat model
3. **Define a Prompt** <5分>
  - 使用 `PromptTemplate` or `ChatPromptTemplate` 創建一個 prompt
  - 這個 prompt 必須包含變數 `question`
4. **Define a Chain** <5分>
  - 使用剛剛定義的 LLM & prompt 創建一個 chain
5. **Invoke the Chain & Print the Answer** <10分>
  - <mark>請用這個問題：`"Are there aliens on the Moon?"`
  - 需用到 `.invoke()`
  - 修改問號處並使用以下程式碼印出結果：

    ```
    answer = ???????
    print(answer.content)
    ```
## Part 2: Customize 3 Math Tools

🔺請依照以下指示，創建 3 個 LangChain 工具 for 基本數學運算：

1. **Install and import necessary libraries**
2. **Define Tools**

    - 請將三個工具分別命名成： `divide`, `minus`, `exponentiate`
    - 使用 `langchain_core.tools` 模組中的 @tool decorator 來定義每個工具，需定義每個工具的參數和回傳類型 <18分>
    - 在工具的函數中編寫程式碼，以執行特定的數學運算 <6分>

        🌟HINTS🌟
      - divide: 第1個整數 除以 第2個整數
      - minus: 第1個整數 減 第2個整數
      - exponentiate: 第1個整數的(第2個整數)次方

3. **Store the Tools** <6分>
  - 請將三個工具以 list 方式，儲存在 `tools` 這個變數

## Part 3: Combine Tools with Agent

🔺請依照以下指示，結合 Part 2 的 `tools` 創建 1 個 agent
0. **請保留 Part 2 儲存的 `tools`**
  - <mark>如果 part 2 part 3 分成兩次做，請先跑一次 part 2 的 code，再繼續執行以下操作
1. **Install and import necessary libraries**
2. **Define an LLM** <5分>
  - 選用一個 HuggingFace 模型


3. **Define Prompt** <20分>
  - 使用 `ChatPromptTemplate.from_messages()` 創造一個 prompt <
  - 這格程式碼會長得像：
    ```python
      prompt = ChatPromptTemplate.from_messages(
        [
          ("¿¿", "❓❓❓",),
          ("placeholder", "❓❓❓"),
          ("¿¿", "❓❓❓"),
          ("placeholder", "{agent_scratchpad}"),
        ]
      )
    ```
  - 當然你也可以自由發揮🐳
  
4. **Define Agent Chain** <15分>
  - 使用 `initialize_agent()` 定義一個 agent chain
  - <mark>可能需要的模組和函數
    ```python
      from langchain.agents import AgentType
      from langchain.agents import initialize_agent
    ```
5. **Invoke Agent Executor** <5分>
  - 使用以下程式碼印出模型的回覆結果
    ```python
      ## invoke agent_executor 列印模型的回覆結果
      result = agent_executor.invoke({
      "input": "Take 2 to the power of 6, then divide this result obtained by the result of 24 minus 8, then square the whole result"
      })

      print(result)
    ```

## BONUS: 針對 YT 影片問問題

1. 使用 [YouTube transcripts Loaders](https://python.langchain.com/v0.1/docs/integrations/document_loaders/youtube_transcript/) 抓取任何「長度大於10分鐘」的 YouTube影片的cc字幕，會讀成一個長文本
2. 將此文本做成向量，存到一個 VectorStore DB （建議使用 [Chroma](https://python.langchain.com/v0.1/docs/integrations/vectorstores/chroma/)）
3. 建立一個 retriever 以及基於此 retriever 的 LLM chain（[助教課的Colab](https://colab.research.google.com/drive/1T7Q4X9qeppvMuYI3pJLN4OfD9L_F6YMx?usp=sharing)有教ㄛ🐳）
4. 設計一個和此影片有關的問題
5. 最後請把  **`chain.invoke('貼上你自己設計的問題')`  的結果列印出來**
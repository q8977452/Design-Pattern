# 橋接 Bridge
可將一個大類或一系列緊密相關的類拆分為抽象和實現兩個獨立的層次結構， 從而能在開發時分別使用
## 優缺點
### 優點
1. 可以創建與平台無關的類和程序

2. 客戶端代碼僅與高層抽象部分進行互動，不會接觸到平台的詳細信息。

3. Single Responsibility Principle

    抽象部分專注於處理高層邏輯， 實現部分處理平台細節

4. Open/Closed Principle

    可以新增抽象部分和實現部分， 且它們之間不會相互影響
    


### 缺點
* 對高內聚的類使用該模式可能會讓代碼更加複雜

## Architecture

![](https://refactoringguru.cn/images/patterns/diagrams/bridge/structure-zh.png?id=8f6df21bea5074e798d6)

1. 抽象部分(Abstraction)

    * 提供高層控制邏輯，依賴於完成底層實際工作的實現對象
    * 通常聲明一些複雜行為

2. 實現部分(Implementation)
    
    * 為所有具體實現聲明通用接口


3. 具體實現(Concrete Implementation)
    
    * 包括特定於平台的代碼
    
4. 精確抽象(Refined Abstraction)

    * 提供控制邏輯的變體
    * 與其父類一樣，它們通過通用實現接口與不同的實現進行交互


5. 客戶端(Client)

    * 僅關心如何與抽象部分合作
    * 需要將抽像對象與一個實現對象連接起來

## 應用場景
* 如果你想要拆分或重組一個具有多重功能的龐雜類
* 如果你希望在幾個獨立維度上擴展一個類
* 如果你需要在運行時切換不同實現方法

## 實現方式
下列七個步驟
1. 明確類中獨立的維度

    * 獨立的概念可能是
        * 抽象/平台
        * 域/基礎設施
        * 前端/後端
        * 接口/實現
    
2. 了解客戶端的業務需求，並在抽象基類中定義它們
    
3. 確定在所有平台上都可執行的業務
    
    * 在通用實現接口中聲明抽象部分所需的業務
    
4. 為你域內的所有平台創建實現類，但需確保它們遵循實現部分的接口
    
5. 在抽像類中添加指向實現類型的引用成員變量

    * 抽象部分會將大部分工作委派給該成員變量所指向的實現對象

6. 如果你的高層邏輯有多個變體，則可通過擴展抽象基類為每個變體創建一個精確抽象

7. 客戶端

    * 代碼必須將實現對像傳遞給抽象部分的構造函數才能使其能夠相互關聯
    * 只需與抽像對象進行交互， 無需和實現對像打交道
# 外觀/門面 Facade
能為程序庫、 框架或其他復雜類提供一個簡單的接口


## 優缺點
### 優點
1. 可以讓自己的代碼獨立於復雜子系統

### 缺點
* 能成為與程序中所有類都耦合的上帝對象

## Architecture

![](https://refactoringguru.cn/images/patterns/diagrams/facade/structure.png?id=258401362234ac77a2aa)

1. 外觀(Facade)

    * 提供了一種訪問特定子系統功能的便捷方式，其了解如何重定向客戶端請求，知曉如何操作一切活動部件

2. 創建附加外觀(Additional Facade)
    
    * 可以避免多種不相關的功能污染單一外觀，使其變成又一個複雜結構
    * 客戶端和其他外觀都可使用附加外觀

3. 複雜子系統(Complex Subsystem)
    
    * 由數十個不同對象構成   
    * 如果要用這些對象完成有意義的工作，你必須深入了解子系統的實現細節，比如按照正確順序初始化對象和為其提供正確格式的數據
    * 子系統類不會意識到外觀的存在， 它們在系統內運作並且相互之間可直接進行交互
    
4. 客戶端(Client)

    * 使用外觀代替對子系統對象的直接調用

## 應用場景
* 如果你需要一個指向複雜子系統的直接接口，且該接口的功能有限
* 如果需要將子系統組織為多層結構

## 實現方式
下列四個步驟
1. 考慮能否在現有子系統的基礎上提供一個更簡單的接口

    * 如果該接口能讓客戶端代碼獨立於眾多子系統類，那麼你的方向就是正確的
    
2. 在一個新的外觀類中聲明並實現該接口

    * 外觀應將客戶端代碼的調用重定向到子系統中的相應對象處
    * 如果客戶端代碼沒有對子系統進行初始化，也沒有對其後續生命週期進行管理，那麼外觀必須完成此類工作
    
3. 如果要充分發揮這一模式的優勢，你必須確保所有客戶端代碼僅通過外觀來與子系統進行交互
    
    * 此後客戶端代碼將不會受到任何由子系統代碼修改而造成的影響，比如子系統升級後，你只需修改外觀中的代碼即可
    
4. 如果外觀變得過於臃腫，你可以考慮將其部分行為抽取為一個新的專用外觀類
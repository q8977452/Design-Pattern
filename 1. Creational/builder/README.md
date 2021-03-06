# 生成器 Builder
1. 使你能夠分步驟創建複雜對象
2. 允許你使用相同的創建代碼生成不同類型和形式的對象

## 優缺點
### 優點
1. 可以分步創建對象， 暫緩創建步驟或遞歸運行創建步驟
    
2. 生成不同形式的產品時， 你可以復用相同的製造代碼

3. Single Responsibility Principle

### 缺點
由於該模式需要新增多個類， 因此代碼整體複雜程度會有所增加。

## Architecture

![](https://refactoringguru.cn/images/patterns/diagrams/builder/structure.png?id=fe9e23559923ea0657aa)

1. 生成器(Builder)

    接口聲明在所有類型生成器中通用的產品構造步驟
    
2. 具體生成器(Concrete Builder)
    
    a. 供構造過程的不同實現
    
    b. 也可以構造不遵循通用接口的產品

3. 產品(Products)

    a. 最終生成的對象
    
    b. 由不同生成器構造的產品無需屬於同一類層次結構或接口
    
4. 主管(Director)
    
    類定義調用構造步驟的順序，這樣你就可以創建和復用特定的產品配置
    
5. 客戶端(Client)

## 應用場景
* 避免 **重疊構造函數（telescopic constructor)** 的出現
* 希望使用代碼創建不同形式的產品
* 構造組合樹或其他復雜對象

## 實現方式
下列六個步驟
1. 清晰地定義通用步驟， 確保它們可以製造所有形式的產品。 否則你將無法進一步實施該模式。

2. 在基本生成器接口中聲明這些步驟。

3. 為每個形式的產品創建具體生成器類， 並實現其構造步驟。

4. 考慮創建主管類。 它可以使用同一生成器對象來封裝多種構造產品的方式。

5. 客戶端代碼會同時創建生成器和主管對象。 構造開始前， 客戶端必須將生成器對像傳遞給主管對象。 通常情況下， 客戶端只需調用主管類構造函數一次即可。 主管類使用生成器對象完成後續所有製造任務。 還有另一種方式， 那就是客戶端可以將生成器對象直接傳遞給主管類的製造方法。

6. 只有在所有產品都遵循相同接口的情況下， 構造結果可以直接通過主管類獲取。 否則， 客戶端應當通過生成器獲取構造結果。
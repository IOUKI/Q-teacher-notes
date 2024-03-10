# 模型評估

# 目錄
1. 訓練模型: 非文字資料前處理
2. 模型評估

# 訓練模型

## 資料預處理

### Data Exemple
<table>
    <tr>
        <td>名稱</td>
        <td>年紀</td>
        <td>喜歡的水果</td>
    </tr>
    <tr>
        <td>阿明</td>
        <td>幼年</td>
        <td>芭樂</td>
    </tr>
    <tr>
        <td>曉華</td>
        <td>少年</td>
        <td>香蕉</td>
    </tr>
    <tr>
        <td>家豪</td>
        <td>中年</td>
        <td>橘子</td>
    </tr>
</table>

### Label Encoding
當資料有高低之分時，可以使用「Label Encoding」，將資料轉成高低數值來區分等級
<table>
    <tr>
        <td>名稱</td>
        <td>年紀</td>
        <td>喜歡的水果</td>
    </tr>
    <tr>
        <td>阿明</td>
        <td>1</td>
        <td>芭樂</td>
    </tr>
    <tr>
        <td>曉華</td>
        <td>2</td>
        <td>香蕉</td>
    </tr>
    <tr>
        <td>家豪</td>
        <td>3</td>
        <td>橘子</td>
    </tr>
</table>

### One-Hot Encoding
將無序的資料轉換成數值特徵顯示，通常會將每個資料展開成一個欄位來顯示，數值為1跟0
<table>
    <tr>
        <td>名稱</td>
        <td>年紀</td>
        <td>喜歡芭樂</td>
        <td>喜歡香蕉</td>
        <td>喜歡橘子</td>
    </tr>
    <tr>
        <td>阿明</td>
        <td>幼年</td>
        <td>1</td>
        <td>0</td>
        <td>0</td>
    </tr>
    <tr>
        <td>曉華</td>
        <td>少年</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
    </tr>
    <tr>
        <td>家豪</td>
        <td>中年</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
    </tr>
</table>

### 整理完的資料

<table>
    <tr>
        <td>名稱</td>
        <td>年紀</td>
        <td>喜歡芭樂</td>
        <td>喜歡香蕉</td>
        <td>喜歡橘子</td>
    </tr>
    <tr>
        <td>阿明</td>
        <td>1</td>
        <td>1</td>
        <td>0</td>
        <td>0</td>
    </tr>
    <tr>
        <td>曉華</td>
        <td>2</td>
        <td>0</td>
        <td>1</td>
        <td>0</td>
    </tr>
    <tr>
        <td>家豪</td>
        <td>3</td>
        <td>0</td>
        <td>0</td>
        <td>1</td>
    </tr>
</table>

### 離群值(outliers)
當有些資料數值離群體態遠，將會引響模型的準確性
> ## 偵測離群值
> ### 當資料為常態分配(normal distribution)
> - 3倍標準差法 (分布對稱)
> - Boxplots法 (分布不對稱)
> ### 當資料不為常態分配
> - 孤立森林(isolation foest)

> ## 主要處理方法
> - 直接刪除: 確認該資料對於資料集來說沒有特殊意義，直接刪除
> - 平均值調整: 利用前後兩個資料點的平均值修正該異常值
> - Z-score Normallization: 將資料減去平均值除已標準差
> - 不處理: 直接擺爛...

> ## 不平衡的資料
> 當訓練集中某一個種類的資料太多，會引響準確率
> ### 主要處理辦法
> - 增加少數類別數據
> - 對數據進行重採樣(resampling):
>> 1. 過採樣: 增加訓練集中少數類別中樣本數量。(缺點: 容易發生過度擬合的現象)
>> 2. 欠採樣: 減少原始數據原始數據集中多數類別的樣本數量。(缺點: 因為他是從原始數據集中刪除觀察結果，因此可能會丟棄有用的訊息)
> - 調整F score的beta值: 依據模型表現和資料，看要偏重precision或是recall。

### 資料正確性
1. tp (True Positive): 表示機器標註正確與正確標註對比，機器「正確」標註為「真」的數據
2. tn (True Negative): 表示機器標註正確與正確標註對比，機器「正確」標註為「假」的數據
3. fp (False Positive): 表示機器標註正確與正確標註對比，機器「錯誤」標註為「真」的數據 (型一錯誤)
4. fn (False Negative): 表示機器標註正確與正確標註對比，機器「錯誤」標註為「假」的數據 (型二錯誤)

<table>
    <tr>
        <td></td>
        <td>True</td>
        <td>False</td>
    </tr>
    <tr>
        <td>Positive</td>
        <td>TP</td>
        <td>FP</td>
    </tr>
    <tr>
        <td>Negative</td>
        <td>FN</td>
        <td>TN</td>
    </tr>
</table>
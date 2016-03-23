# javascript-style-guide-translate

Translate and Collect from other javascript style guide.

主要為翻譯與收集來自其他的Javascript風格指引的文件。

## 列表 List

- [Khan Academy Coding Style Guides](https://github.com/Khan/style-guides)
- [Airbnb React/JSX style guide](https://github.com/airbnb/javascript/tree/master/react)
- [React Style Guide](https://github.com/kriasoft/react-starter-kit/blob/master/docs/react-style-guide.md)

## 動機 Motivation

技術文件不同於一些的文件或文章，它有其特別領域的專業，對於翻譯者而言，除了本身的英文閱讀能力要足夠外，還要求要有一定的專業程度。網路上有許多文件被翻譯成為中文，有可能是繁體中文或簡體中文，或是由簡體中文直接轉譯為繁體中文，但其中的翻譯品質常出現很大的問題，除了其內容與英文原意可能不同外，甚至出現無法使用中文來閱讀理解的情況。

這份資料是希望能用比較好的方式進行技術原文的翻譯，主要的領域是著重在Javascript、React相關的入門文件與指引。

## 翻譯指引 Translation Guide

翻譯的指引通用於所有文件的翻譯，提供一些翻譯上的指引。

### 始終不改變原文原意

翻譯的目的是對於原文的原意，儘可能翻譯其內容涵意，可視情況縮短或增長說明文字。但始終不進行原文的原意進行刪減或額外增加。

需增加額外的解說，需用"譯者註"在後面加註說明，代表這是由譯者額外增加的。例如原文可能有誤或提供更多額外的資訊。為保持原文原意，譯者註儘可能簡潔與少使用。

如果對原文所說明的內容，以翻譯者的專業尚難以理解，儘可能保留原文。

儘可能翻譯所有原文為中文，不要過度出現中英文混雜的使用情況。

### 專有名詞

對於專有名詞，例如函式庫中的定義、函式、方法、物件等專用名詞，保留原字詞不進行"取代式"的翻譯，而使用括號(())加註其後作為補充翻譯，例如：

```
state(狀態)
props(屬性)
```

對於專用術語、形容詞、或可能通用的一詞多義的英文字詞，翻譯其字詞，但使用括號(())將原英文字詞加註其後，作為補充，例如：

原文字句：

```
Use PascalCase for React components and camelCase for their instances.
```

中文翻譯字句：

```
對React元件使用巴斯卡(PascalCase)命名法，它們的實例則使用小駝峰(camelCase)命名法。
```

### 符號

對於在原文解釋用句中，所提供的符號，儘可能在翻譯時使用括號(())加註符號在翻譯字句中。例如：

原文字句：

```
Always use double quotes (") for JSX attributes, but single quotes for all other JS
```

中文翻譯字句：

```
對JSX的屬性，必定使用雙引號(")，而對其他的JS語法則使用單引號(')。
```

### 程式碼註解

程式碼註解可以翻譯，但程式碼註解有時過於簡略時也可以略去不翻譯。

### 中文字詞與符號

可以使用全形的逗號(，)、分號(、)與句號(。)，但儘量不使用用全形的括號(（）)、框號(「」)與其他符號等。而是使用原文提供的半形符號。

適當的在中文字詞的前後加上空白字元，作為明顯的區隔出這個字詞。例如：

```
使用 擴充套件->管理 進入這個管理的頁面。
```

不要使用過短的文言式字詞來作翻譯，儘可能以較合理的解譯方式來翻譯。例如：

原文字句：

```
Reusable Components
```

不好的中文翻譯字句：

```
可重用元件
```

較佳的中文翻譯字句：

```
可重覆使用的元件
```

不要使用過長的中文字句，儘可能多使用逗號(，)或句號(。)分隔翻譯字句以方便閱讀。例如：

原文字句：

```
Use computed property names when creating objects with dynamic property names.
```

不好的中文翻譯字句：

```
建立具有動態屬性名稱的物件時請使用計算型的屬性名稱。
```

較佳的中文翻譯字句：

```
在建立帶有動態屬性名稱的物件時，使用計算型屬性(computed property)名稱。
```

### 繁體與簡體中文字詞

不要直接把簡體中文翻譯字詞，直接套用到繁體中文翻譯字詞上，而應該儘可能轉換為常用的專門名詞。。例如以下常見的對照字詞：

```
數據庫 vs 資料庫
组件 vs 元件
用戶 vs 使用者
默認 vs 預設
代碼 vs 程式碼
視頻 vs 影片
```

## 更新日誌 Changlog

- 2016/3/22 加入 [Khan Academy Coding Style Guides](https://github.com/Khan/style-guides)之Javascript與React
- 2016/3/21 加入與完成翻譯 [Airbnb React/JSX style guide](https://github.com/airbnb/javascript/tree/master/react)
- 2016/3/21 加入與完成翻譯 [React Style Guide](https://github.com/kriasoft/react-starter-kit/blob/master/docs/react-style-guide.md)


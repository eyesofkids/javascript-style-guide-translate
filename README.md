# javascript-style-guide-translate

主要為翻譯與收集來自其他的Javascript風格指引的文件。

## 列表 List

- [Khan Academy Coding Style Guides](https://github.com/Khan/style-guides)
- [Airbnb React/JSX style guide](https://github.com/airbnb/javascript/tree/master/react)
- [React Style Guide](https://github.com/kriasoft/react-starter-kit/blob/master/docs/react-style-guide.md)

## 動機

軟體技術文件不同於一般的科技文件或文章，它有其特別領域的專業，對於翻譯者而言，除了本身的英文閱讀能力要足夠外，還要求要有一定的專業程度。網路上有許多文件被翻譯成為中文，有可能是繁體中文或簡體中文，或是由簡體中文直接轉譯為繁體中文，但其中的翻譯品質常出現很大的問題，除了其內容與英文原意可能不同外，甚至出現無法使用中文來閱讀理解的情況。

這份資料是希望能用比較好的方式進行技術原文的翻譯，主要的領域是著重在Javascript、React相關的入門文件與指引。

## 翻譯指引

翻譯的指引通用於所有文件的翻譯，提供一些翻譯上的指引。

### 始終不改變原文原意

翻譯的目的是對於原文的原意，儘可能翻譯其內容涵意，可視情況縮短或增長說明文字，但始終不對原文的原意進行刪減或額外增加。

需增加額外的解說，需用"譯者註"在後面加註說明，代表這是由譯者額外增加的。例如原文可能有誤或提供更多額外的資訊。為保持原文原意的完整，譯者註儘可能簡潔與少使用。

如果對原文所說明的內容，以翻譯者的專業尚難以理解，儘可能保留原文，以加註類似於"本文因原文涵意譯者尚無法理解，因此保留原文"的字句於文章最上方。

儘可能翻譯所有原文為中文，不要過度出現中英文混雜的使用情況。

### 專有名詞

對於專有名詞，例如函式庫中的定義、函式、方法、物件、API、關鍵字等專用名詞，保留原字詞不進行"取代式"的翻譯，而使用括號(())加註其後作為補充翻譯，專有名語可以使用粗體、空格分隔明顯區分，例如：

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
對React元件使用 巴斯卡(PascalCase) 命名法，它們的實例則使用 小駝峰(camelCase) 命名法。
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

### 標題

文章的標題可視情況進行翻譯，但較好的作法是保留原文字詞，並於其後加註中文翻譯。

### 音標

可以使用中文或混用英文標註英文發音，使用斜線符號(//)框住音標註記，例如:

```
const/康死/ 是 英文constant/康死撐/ 的簡寫。
```

### 複數

當英文中使用複數或有集合類的字詞時，使用中文擬人化的"們"或副詞"這些"、"那些"、"多個"等附加詞，讓讀者理解這是集合類或複數的名詞，例如:

```
If your component has multi-line properties, close its tag on a new line
```

中譯為:

```
如果你的元件有多行的多個屬性時，在新的下一行在封閉它的標記。
```

### 省略的主詞

當英文中的主詞被省略時，或是要分拆過長的英文語句時，可以再加上原先的主詞，讓翻譯字句表達得更清楚明確。

### 未來、過去、現在進行式與時間順序

英文中有使用`will`通常為未來式，過去式的形態雖然也常用於被動會比較不明確，但過去式有代表已完成的意涵，現在進行式與單使用動作的動詞類似語法。

代表時間通常會有`when`、`before`、`after`等介系詞，在中譯時要注意順序，通常如果是出現倒裝句，會有較為重點的說明會在前面。

```
render()

The render() method is required.

When called, it should examine this.props and this.state and return a single React element. This element can be either a representation of a native DOM component, such as <div />, or another composite component that you've defined yourself.
```

中譯

```
render()

render方法是必要的。

當render被呼叫時，它應該會對this.props與this.state進行檢查，然後回傳單一個React元素。這元件
可能是一個對原生DOM元件的真實呈現，例如<div />，或是另一個你自行定義的合成元件。

```

### 重覆贅詞/不需要的冠名詞

在一句英文語句中，重覆的贅詞可以不需要完全翻譯，可以在充份已表達意思時，去除這些贅詞。通常`The`, `This`, `These`等冠名詞，經常也不需要翻譯。例如:

```
Your components tell React what you want to render – then React will efficiently update and render just the right components when your data changes.
```

完整的中譯文為:

```
你的元件告訴React你想要渲染什麼 - 然後當你的資料更動時，React將會有效地更新與渲染必要的元件。
```

"你的"、"你"重覆過多，去除某幾個之後的調整後中譯文:

```
你的元件告訴React想要渲染什麼 - 然後當資料更動時，React將會有效地更新與渲染必要的元件。
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

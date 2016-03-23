## React 風格指引

----
* [Syntax](#syntax)
  * [Order your methods with lifecycle first and render last.](#order-your-methods-with-lifecycle-first-and-render-last)
  * [Name handlers handleEventName.](#name-handlers-handleeventname)
  * [Name handlers in props onEventName.](#name-handlers-in-props-oneventname)
  * [Open elements on the same line.](#open-elements-on-the-same-line)
  * [Align and sort HTML properties.](#align-and-sort-html-properties)
  * [Only export a single react class.](#only-export-a-single-react-class)
* [Language features](#language-features)
  * [Make "presentation" components pure.](#make-presentation-components-pure)
  * [Prefer <a href="http://facebook.github.io/react/docs/interactivity-and-dynamic-uis.html#what-components-should-have-state">props to state</a>.](#prefer-props-to-state)
  * [Use <a href="http://facebook.github.io/react/docs/reusable-components.html">propTypes</a>.](#use-proptypes)
  * [<em>Never</em> store state in the DOM.](#never-store-state-in-the-dom)
* [Server-side rendering](#server-side-rendering)
  * [Props must be plain JSON](#props-must-be-plain-json)
  * [Pure functions of props and state](#pure-functions-of-props-and-state)
  * [Side effect free until `componentDidMount`](#side-effect-free-until-componentdidmount)
* [React libraries and components](#react-libraries-and-components)
  * [Do not use Backbone models.](#do-not-use-backbone-models)
  * [Minimize use of jQuery.](#minimize-use-of-jquery)
  * [Reuse standard components.](#reuse-standard-components)

----

> 遵循一般的[JavaScript風格指引](javascript.md) - 包含一行80字元的限制。此外，還有許多React專有的規則。

除了這些風格規則外，你可能也會對這篇文章有興趣
[React best practices](https://docs.google.com/document/d/1ChtFUao18IyNhaXZ5sE2W-CFuFcYnqlFTyi5gfe6XV0/edit).

----------
### 語法

#### 依照順序排序你的方法，lifecycle(生命週期)放前面，render(渲染)放在最後面。

在你的react元件中，你應該依照順序排序方法，例如這樣:

1. lifecycle(生命週期)方法 (按照時間的先後順序:
      `getDefaultProps`,
      `getInitialState`,
      `componentWillMount`,
      `componentDidMount`,
      `componentWillReceiveProps`,
      `shouldComponentUpdate`,
      `componentWillUpdate`,
      `componentDidUpdate`,
      `componentWillUnmount`)
2. 其他的程式碼
3. `render`

#### 用`handleEventName`來命名handlers(處理程序) .

例如:

```jsx
<Component onClick={this.handleClick} onLaunchMissiles={this.handleLaunchMissiles} />
```

#### 用`onEventName`來命名在props(屬性)中的handlers(處理程序)  .

這與React的事件命名方式是一致的: `onClick`, `onDrag`,
`onChange`, 等等。

例如:

```jsx
<Component onLaunchMissiles={this.handleLaunchMissiles} />
```


#### 開頭元素放在同一行

一行80個字元的限制是有點緊湊，所以我們選擇保留額外的4個。

Yes:
```jsx
return <div>
   ...
</div>;
```

No:
```jsx
return (      // "div" 沒放在和 "return" 同一行
    <div>
        ...
    </div>
);
```

#### 對齊與排序HTML屬性

如果可以的話，將它們都放在同一行。如果沒辦法的話，把每個屬性獨立自己一行放置，並縮排4個空白字元，依序放置。封閉尖括號(>)應該也要自己獨立一行，縮排則和開頭的尖括號(<)一致。這樣作可以很容易的對屬性一目瞭然。

Yes:
```jsx
<div className="highlight" key="highlight-div">
<div
    className="highlight"
    key="highlight-div"
>
<Image
    className="highlight"
    key="highlight-div"
/>
```

No:
```jsx
<div className="highlight"      // property not on its own line
     key="highlight-div"
>
<div                            // closing brace not on its own line
    className="highlight"
    key="highlight-div">
<div                            // property is not sorted
    key="highlight-div"
    className="highlight"
>
```

#### 只export(輸出)單一個react類別

每個.jsx檔案應該只會輸出單一個React類別，不會有其他的。
這是為了有可測試性；fixture框架會要求它功能。

注意檔案中仍然可以定義多個類別，但它不能輸出超過一個以上。

---------------------
### 語言特性

#### 讓"presentation(呈現)"元件保持純粹(pure)

思考把React的世界區分成["logic"
components 與 "presentation" components](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)是很有好處的。

"Logic(邏輯)"元件有應用程式的邏輯，但它們本身不會產出HTML。

"Presentation(呈現)"元件是典型地可重覆使用的，以及的確會產出HTML。

Logic(邏輯)元件可以有內部的state(狀態)，但presentation(呈現)元件則完全不會有。

#### 建議使用[props(屬性)而不是state(狀態)](http://facebook.github.io/react/docs/interactivity-and-dynamic-uis.html#what-components-should-have-state).

You almost always want to use props. By avoiding state when possible,
you minimize redundancy, making it easier to reason about your
application.

A common pattern — which matches the "logic" vs. "presentation"
component distinction — is to create several stateless components
that just render data, and have a stateful component above them in the
hierarchy that passes its state to its children via props. The
stateful component encapsulates all of the interaction logic, while
the stateless components take care of rendering data in a declarative
way.

Copying data from props to state can cause the UI to get out of sync
and is especially bad.

#### 使用[propTypes](http://facebook.github.io/react/docs/reusable-components.html).

React元件應該一定有完整的`propTypes`。每個`this.props`的屬性應該在`propTypes`裡有相對應的登錄項目。This documents that props need to be passed to a model.
([example](https://github.com/Khan/webapp/blob/32aa862769d4e93c477dc0ee0388816056252c4a/javascript/search-package/search-results-list.jsx#L14))

If you are passing data through to a child component, you can use
the prop-type `<child-class>.propTypes.<prop-name>`.

Avoid these non-descriptive prop-types:
   * `React.PropTypes.any`
   * `React.PropTypes.array`
   * `React.PropTypes.object`

Instead, use
   * `React.PropTypes.arrayOf`
   * `React.PropTypes.objectOf`
   * `React.PropTypes.instanceOf`
   * `React.PropTypes.shape`

As an exception, if you are passing data through to a child component,
and you can't use `<child-class>.propTypes.<prop-name>` for some
reason, you can use `React.PropType.any`.

#### *絕對不要* 儲存state(狀態)在DOM裡面

Do not use `data-` attributes or classes. All information
should be stored in JavaScript, either in the React component itself,
or in a React store if using a framework such as Redux.

----------------------------------

### 伺服器端的渲染(rendering)

To make components safe to render server-side, they must adhere
to a few more restrictions than regular components.

#### Props must be plain JSON

In order to render server-side, the props are serialized and
deserialized from JSON. This means that e.g. dates must be
passed as timestamps as opposed to JS `Date` objects.

Note that this only applies to the root component being
rendered with server-side rendering. If the root component
constructs more complex data structures from props, and
passes those constructs down to child components, that won't
cause problems.

#### Pure functions of props and state

Components must be pure functions of their `props` and `state`.
This means the output of their `render()` function must not
depend on either KA-specific globals, on browser-specific
state, or browser-specific APIs.

Examples of KA-specific globals include anything attached to
the `KA` global, e.g. `KA.getUserId()`, or data extracted from
the DOM such as `data-` properties attached to other DOM nodes.

Examples of browser-specific state include the user agent,
the screen resolution, the device pixel density etc. 

An example of a browser-specific API is `canvas.getContext()`.

The output must be deterministic. One way to get
non-deterministic output is to generate random
IDs in `getInitialState()`, and have the output
of render depend on that ID. Don't do this.

#### Side effect free until `componentDidMount`

The parts of the React component lifecycle that are run to
render on the server must be free from side effects.

Examples of side effects that must be avoided:
- Sending an AJAX request
- Mutating global JS state
- Injecting elements into the DOM
- Changing the page title
- `alert()`

The lifecycle methods that run on the server are currently:

- `getInitialState()`
- `getDefaultProps()`
- `componentWillMount()`
- `render()`

If you need to execute any of the above listed side effects,
you must do so in `componentDidMount` or later in the component
lifecycle. These functions are not executed server-side.

----------------------------------
### React 函式庫與元件

#### 不要使用Backbone的models

使用flux的actions(動作)，或是直接使用`$.ajax`作為取代。

我們試著要從我們的codebase整個移除掉Backbone。

#### 儘可能最低限度的使用jQuery.

*絕對不要* 使用jQuery來作DOM的操作處理。

試著避免使用jQuery外掛。真的有需要時，用一個React元件包裹jQuery外掛，這樣你只需要接觸到jQuery一次。

你可以使用`$.ajax` (但不要用其他的函式，例如`$.post`) 來進行網路的通訊。

#### 重覆使用標準的元件

If possible, re-use existing components, especially low-level, pure
components that emit HTML directly. If you write a new such one, and
it finds a use in a different project, put it in a shared location
such as the react.js package.

The standard shared location for useful components that have been
open sourced is the `react-components.js` package in
`javascript-packages.json`. This includes components such as these:

* `SetIntervalMixin` - provides a setInterval method so something can be
  done every x milliseconds
* `$_` - the i18n wrapper to allow for translating text in React.
* `TimeAgo` - “five minutes ago”, etc - this replaces $.timeago

Reusable components that have not (yet) been open sourced are in the
(poorly named) `react.js` package.  This include components such as
these:

* `KUIButton` - render a Khan Academy styled button.
* `Modal` - create a modal dialog.

This list is far from complete.

### 

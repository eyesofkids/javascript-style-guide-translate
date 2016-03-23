# Airbnb React/JSX Style Guide

*A mostly reasonable approach to React and JSX*

## Table of Contents

  1. [基本規則](#basic-rules)
  1. [Class vs `React.createClass` vs stateless](#class-vs-reactcreateclass-vs-stateless)
  1. [命名](#naming)
  1. [宣告](#declaration)
  1. [對齊](#alignment)
  1. [引號](#quotes)
  1. [空白](#spacing)
  1. [屬性(Props)](#props)
  1. [括號](#parentheses)
  1. [標籤](#tags)
  1. [方法](#methods)
  1. [順序](#ordering)
  1. [`isMounted`](#ismounted)

## 基本規則

  - 每個程式碼檔案中只會包含一個React元件(component)
    - 不過，多個[無狀態、純粹的元件](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions) 同時寫在一個檔案中是允許的。eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
  - 必定使用 JSX 語法。
  - 不要使用 `React.createElement` ，除非你需要從一個不是JSX檔案來初始化應用程式。


## 類別(Class) vs `React.createClass` vs 無狀態(stateless)

  - 如果你會有內部的 state(狀態) 與/或 refs(參照)，用 `class extends React.Component` 會比 `React.createClass` 更好，除非你有非常需要使用 mixins(混入) 的理由。eslint: [`react/prefer-es6-class`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-es6-class.md) [`react/prefer-stateless-function`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-stateless-function.md)

> 譯者註：ES6 Class的對於Mixins解決方式，可參考[Mixins Are Dead. Long Live Composition](https://medium.com/@dan_abramov/mixins-are-dead-long-live-higher-order-components-94a0d2f9e750#.toy96djeg)


    ```javascript
    // bad
    const Listing = React.createClass({
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    });

    // good
    class Listing extends React.Component {
      // ...
      render() {
        return <div>{this.state.hello}</div>;
      }
    }
    ```

    而如果你並沒有用到 state 或 refs，建議連類別都不用了，使用一般的函式就好(不要用箭頭函式(arrow functions)):

    ```javascript

    // bad
    class Listing extends React.Component {
      render() {
        return <div>{this.props.hello}</div>;
      }
    }

    // bad (since arrow functions do not have a "name" property)
    const Listing = ({ hello }) => (
      <div>{hello}</div>
    );

    // good
    function Listing({ hello }) {
      return <div>{hello}</div>;
    }
    ```

## 命名

  - **副檔名**: React元件檔案使用`.jsx`副檔名。
  - **檔案名稱**: 檔案名稱使用巴斯卡(PascalCase)命名法。例如`ReservationCard.jsx`。
  - **引用(Reference)命名**: React元件使用巴斯卡(PascalCase)命名法，它們的實例則使用小駝峰(camelCase)命名法。eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

    ```javascript
    // bad
    import reservationCard from './ReservationCard';

    // good
    import ReservationCard from './ReservationCard';

    // bad
    const ReservationItem = <ReservationCard />;

    // good
    const reservationItem = <ReservationCard />;
    ```

  - **元件命名**: 檔案名稱與元件名稱相同。例如`ReservationCard.jsx`應該有個引用名稱`ReservationCard`。不過，如果這是在一個目錄中的根(root)元件，則使用`index.jsx`作為檔案名稱，然後使用目錄名稱作為元件名稱:

    ```javascript
    // bad
    import Footer from './Footer/Footer';

    // bad
    import Footer from './Footer/index';

    // good
    import Footer from './Footer';
    ```

## 宣告(Declaration)

  - 不要使用`displayName`來命名元件。而是用引用(reference)來命名元件。

    ```javascript
    // bad
    export default React.createClass({
      displayName: 'ReservationCard',
      // stuff goes here
    });

    // good
    export default class ReservationCard extends React.Component {
    }
    ```

## 對齊

  - 遵守JSX語法中的那些對齊樣式。eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

    ```javascript
    // bad
    <Foo superLongParam="bar"
         anotherSuperLongParam="baz" />

    // good
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    />

    // if props fit in one line then keep it on the same line
    <Foo bar="bar" />

    // children get indented normally
    <Foo
      superLongParam="bar"
      anotherSuperLongParam="baz"
    >
      <Quux />
    </Foo>
    ```

## 引號

  - 對JSX的屬性，必定使用雙引號(`"`)，而對其他的JS語法則使用單引號(`'`)。eslint: [`jsx-quotes`](http://eslint.org/docs/rules/jsx-quotes)

  > 為什麼? 因為JSX屬性 [無法包含跳脫引號](http://eslint.org/docs/rules/jsx-quotes)，所以雙引號才能配合像`"don't"`這樣的輸入字詞。
  > 一般的HTML屬性也習慣上會使用雙引號，而不使用單引號，所以JSX屬性也使用這個慣例。
  
  ```javascript
    // bad
    <Foo bar='bar' />

    // good
    <Foo bar="bar" />

    // bad
    <Foo style={{ left: "20px" }} />

    // good
    <Foo style={{ left: '20px' }} />
    ```

## 空白

  - 必定包含一個單格空白在你的自封閉標籤(/>)。

    ```javascript
    // bad
    <Foo/>

    // very bad
    <Foo                 />

    // bad
    <Foo
     />

    // good
    <Foo />
    ```

## Props(屬性)

  - 必定使用小駝峰(camelCase)命名法來命名prop(屬性)名稱。

    ```javascript
    // bad
    <Foo
      UserName="hello"
      phone_number={12345678}
    />

    // good
    <Foo
      userName="hello"
      phoneNumber={12345678}
    />
    ```

  - 當prop(屬性)是明確的`true`數值時，省略它的數值。eslint: [`react/jsx-boolean-value`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-boolean-value.md)

    ```javascript
    // bad
    <Foo
      hidden={true}
    />

    // good
    <Foo
      hidden
    />
    ```

## 括號

  - 用括號括住JSX標籤，當它們的程式碼超過一行時。eslint: [`react/wrap-multilines`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/wrap-multilines.md)

    ```javascript
    // bad
    render() {
      return <MyComponent className="long body" foo="bar">
               <MyChild />
             </MyComponent>;
    }

    // good
    render() {
      return (
        <MyComponent className="long body" foo="bar">
          <MyChild />
        </MyComponent>
      );
    }

    // good, when single line
    render() {
      const body = <div>hello</div>;
      return <MyComponent>{body}</MyComponent>;
    }
    ```

## 標籤(Tags)

  - 當沒有子元素時，必定使用自封閉標籤(/>)。eslint: [`react/self-closing-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)

    ```javascript
    // bad
    <Foo className="stuff"></Foo>

    // good
    <Foo className="stuff" />
    ```

  - 當你的元件有多行屬性時，將封閉標籤放在新的一行。eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

    ```javascript
    // bad
    <Foo
      bar="bar"
      baz="baz" />

    // good
    <Foo
      bar="bar"
      baz="baz"
    />
    ```

## 方法(Methods)

  - 在建構式(constructor)中綁定(Bind)事件處理函式。 eslint: [`react/jsx-no-bind`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-bind.md)

  > 為什麼? 放在render路徑中的綁定(bind)呼叫，在每次render時都會建立全新的函式。

    ```javascript
    // bad
    class extends React.Component {
      onClickDiv() {
        // do stuff
      }

      render() {
        return <div onClick={this.onClickDiv.bind(this)} />
      }
    }

    // good
    class extends React.Component {
      constructor(props) {
        super(props);

        this.onClickDiv = this.onClickDiv.bind(this);
      }

      onClickDiv() {
        // do stuff
      }

      render() {
        return <div onClick={this.onClickDiv} />
      }
    }
    ```

  - 不要使用下底線(_)前綴字在React元件內部的方法。

    ```javascript
    // bad
    React.createClass({
      _onClickSubmit() {
        // do stuff
      },

      // other stuff
    });

    // good
    class extends React.Component {
      onClickSubmit() {
        // do stuff
      }

      // other stuff
    }
    ```

## 順序

  - 在`class extends React.Component`裡依照以下的順序:

  1. 可選擇的 `static` methods
  1. `constructor`
  1. `getChildContext`
  1. `componentWillMount`
  1. `componentDidMount`
  1. `componentWillReceiveProps`
  1. `shouldComponentUpdate`
  1. `componentWillUpdate`
  1. `componentDidUpdate`
  1. `componentWillUnmount`
  1. *clickHandlers or eventHandlers* like `onClickSubmit()` or `onChangeDescription()`
  1. *getter methods for `render`* like `getSelectReason()` or `getFooterContent()`
  1. *Optional render methods* like `renderNavigation()` or `renderProfilePicture()`
  1. `render`

  - 如何定義`propTypes`, `defaultProps`, `contextTypes`, 等等...

    ```javascript
    import React, { PropTypes } from 'react';

    const propTypes = {
      id: PropTypes.number.isRequired,
      url: PropTypes.string.isRequired,
      text: PropTypes.string,
    };

    const defaultProps = {
      text: 'Hello World',
    };

    class Link extends React.Component {
      static methodsAreOk() {
        return true;
      }

      render() {
        return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>
      }
    }

    Link.propTypes = propTypes;
    Link.defaultProps = defaultProps;

    export default Link;
    ```

  - 在`React.createClass`裡依照以下的順序: eslint: [`react/sort-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/sort-comp.md)

  1. `displayName`
  1. `propTypes`
  1. `contextTypes`
  1. `childContextTypes`
  1. `mixins`
  1. `statics`
  1. `defaultProps`
  1. `getDefaultProps`
  1. `getInitialState`
  1. `getChildContext`
  1. `componentWillMount`
  1. `componentDidMount`
  1. `componentWillReceiveProps`
  1. `shouldComponentUpdate`
  1. `componentWillUpdate`
  1. `componentDidUpdate`
  1. `componentWillUnmount`
  1. *clickHandlers or eventHandlers* like `onClickSubmit()` or `onChangeDescription()`
  1. *getter methods for `render`* like `getSelectReason()` or `getFooterContent()`
  1. *Optional render methods* like `renderNavigation()` or `renderProfilePicture()`
  1. `render`

## `isMounted`

  - 不要使用`isMounted`. eslint: [`react/no-is-mounted`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-is-mounted.md)

  > 為什麼? [`isMounted`是個反模式][anti-pattern]，在當使用ES6類別時是無法使用的，在後面發展途中將會被官方棄用。

  [anti-pattern]: https://facebook.github.io/react/blog/2015/12/16/ismounted-antipattern.html

**[⬆ back to top](#table-of-contents)**

## React 風格指引

> 這份風格指引是來自額外增加於[Airbnb React/JSX Guide](https://github.com/airbnb/javascript/tree/master/react)。
> 你可以自由修改它來適合於你的專案需求。

### 目錄

* [每個UI元件分別使用不同資料夾](#每個UI元件分別使用不同資料夾)
* [建議使用函式型的元件](#建議使用函式型的元件)
* [使用CSS模組](#使用CSS模組)
* [使用higher-order components](#使用higher-order components)

### 每個UI元件分別使用不同資料夾

* 將每個主要UI元件以及它的資源，放置在單獨的分隔資料夾中<br>
  這讓你可以很容易的找到，對任何一個特定UI元素所使用的相關資源 (CSS、圖片、unit tests、本地化檔案等等)。當在重構(refactor)時，要移除這些元件也應該會很容易。
* 避免存在多個元件間共享的CSS、圖片或其他資源檔案。<br>
  這將讓你的程式碼更容易維護，也容易進行重構(refactor)。
* 加入`package.json`到每個元件的資料夾中。<br>
  這可以更容易地參照到其他在你的程式碼中放在別處的元件。<br>
  `import Nav from '../Nav'` vs `import Nav from '../Nav/Nav.js'`

```
/components/Navigation/icon.svg
/components/Navigation/Navigation.css
/components/Navigation/Navigation.js
/components/Navigation/Navigation.test.js
/components/Navigation/Navigation.ru-RU.css
/components/Navigation/package.json
```

```
// components/Navigation/package.json 
{
  "name:": "Navigation",
  "main": "./Navigation.js"
}
```

更多資訊請google查詢[component-based UI development](https://google.com/search?q=component-based+ui+development).

### 建議使用函式型的元件

* 建議儘可能的使用stateless(無狀態的)函式型元件。<br>
  沒有state(狀態)的元件，比較好寫成一個簡單的純函式。

```jsx
// Bad
class Navigation extends Component {
  static propTypes = { items: PropTypes.array.isRequired };
  render() {
    return <nav><ul>{this.props.items.map(x => <li>{x.text}</li>)}</ul></nav>;
  }
}

// Better
function Navigation({ items }) {
  return (
    <nav><ul>{items.map(x => <li>{x.text}</li>)}</ul></nav>;
  );
}
Navigation.propTypes = { items: PropTypes.array.isRequired };
```

### 使用CSS模組(Modules)

* 使用CSS模組<br>
  這將可以使用簡短的CSS類別名稱，以及同時間可避免衝突。
* 保持CSS簡單而且是敘述式的。避免迴圈、混入(mixins)等等。
* 請自由使用在CSS中的變數，透過[precss](https://github.com/jonathantneal/precss) 外掛於[PostCSS](https://github.com/postcss/postcss)
* 建議使用CSS類別選擇器(selectors)，而不要使用元素與`id`選擇器(請見[BEM](https://bem.info/))
* 避免巢狀的CSS選擇器(selectors)(請見[BEM](https://bem.info/))
* 當有疑慮時，使用`.root { }`類別名稱給你元件的root元素。

```scss
// Navigation.scss
@import '../variables.scss';

.root {
  width: 300px;
}

.items {
  margin: 0;
  padding: 0;
  list-style-type: none;
  text-align: center;
}

.item {
  display: inline-block;
  vertical-align: top;
}

.link {
  display: block;
  padding: 0 25px;
  outline: 0;
  border: 0;
  color: $default-color;
  text-decoration: none;
  line-height: 25px;
  transition: background-color .3s ease;

  &,
  .items:hover & {
    background: $default-bg-color;
  }

  .selected,
  .items:hover &:hover {
    background: $active-bg-color;
  }
}
```

```jsx
// Navigation.js
import React, { PropTypes } from 'react';
import withStyles from 'isomorphic-style-loader/lib/withStyles';
import s from './Navigation.scss';

function Navigation() {
  return (
    <nav className={`${s.root} ${this.props.className}`}>
      <ul className={s.items}>
        <li className={`${s.item} ${s.selected}`}>
          <a className={s.link} href="/products">Products</a>
        </li>
        <li className={s.item}>
          <a className={s.link} href="/services">Services</a>
        </li>
      </ul>
    </nav>
  );
}

Navigation.propTypes = { className: PropTypes.string };

export default withStyles(Navigation, s);
```

### 使用higher-order components

* 使用higher-order components (HOC)來繼承(extend)已存在的React元件。<br>
  以下是一個範例:

```js
// withViewport.js
import React, { Component } from 'react';
import { canUseDOM } from 'fbjs/lib/ExecutionEnvironment';

function withViewport(ComposedComponent) {
  return class WithViewport extends Component {

    state = {
      viewport: canUseDOM ?
        {width: window.innerWidth, height: window.innerHeight} :
        {width: 1366, height: 768} // Default size for server-side rendering
    };

    componentDidMount() {
      window.addEventListener('resize', this.handleResize);
      window.addEventListener('orientationchange', this.handleResize);
    }

    componentWillUnmount() {
      window.removeEventListener('resize', this.handleResize);
      window.removeEventListener('orientationchange', this.handleResize);
    }

    handleResize = () => {
      let viewport = {width: window.innerWidth, height: window.innerHeight};
      if (this.state.viewport.width !== viewport.width ||
        this.state.viewport.height !== viewport.height) {
        this.setState({ viewport });
      }
    };

    render() {
      return <ComposedComponent {...this.props} viewport={this.state.viewport}/>;
    }

  };
};

export default withViewport;
```

```js
// MyComponent.js
import React from 'react';
import withViewport from './withViewport';

class MyComponent {
  render() {
    let { width, height } = this.props.viewport;
    return <div>{`Viewport: ${width}x${height}`}</div>;
  }
}

export default withViewport(MyComponent);
```

**[⬆ 回到最上面](#目錄)**

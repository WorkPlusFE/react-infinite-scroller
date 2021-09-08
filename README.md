React Infinite Scroller
=======================

## ⚠️⚠️ 必读 

该 Fork 主要是处理在高版本 Chrome 上，`flex-direction: column-reverse`会使父级组件的`scrollTop`变成负数，基于此，主要对`isReverse`开启的时候，进行了比较粗暴的处理，以保证滚动页面的计算不会出错。

以上，该项目主要用于 WorkPlusFE 内部。

[![npm version](https://badge.fury.io/js/@w6s%2Freact-infinite-scroller.svg)](https://badge.fury.io/js/@w6s%2Freact-infinite-scroller)


```
# npm
npm install @w6s/react-infinite-scroller --save

# yarn
yarn add @w6s/react-infinite-scroller
```

<hr/>


[![Travis](https://img.shields.io/travis/danbovey/react-infinite-scroller.svg?style=flat-square)](https://travis-ci.org/CassetteRocks/react-infinite-scroller)
[![npm](https://img.shields.io/npm/dt/react-infinite-scroller.svg?style=flat-square)](https://www.npmjs.com/package/react-infinite-scroller)
[![React Version](https://img.shields.io/badge/React-%5E0.14.9%20%7C%7C%20%5E15.3.0%20%7C%7C%20%5E16.0.0-blue.svg?style=flat-square)](https://www.npmjs.com/package/react)
[![npm](https://img.shields.io/npm/v/react-infinite-scroller.svg?style=flat-square)](https://www.npmjs.com/package/react-infinite-scroller)
[![npm](https://img.shields.io/npm/l/react-infinite-scroller.svg?style=flat-square)](https://github.com/danbovey/react-infinite-scroller/blob/master/LICENSE)

Infinitely load content using a React Component. This fork maintains a simple, lightweight infinite scroll package that supports both `window` and scrollable elements.

- [Demo](https://danbovey.uk/react-infinite-scroller/demo/)
- [Demo Source](https://github.com/danbovey/react-infinite-scroller/blob/master/docs/src/index.js)

## Installation

```
npm install react-infinite-scroller --save
```
```
yarn add react-infinite-scroller
```

## How to use

```js
import InfiniteScroll from 'react-infinite-scroller';
```

### Window scroll events

```js
<InfiniteScroll
    pageStart={0}
    loadMore={loadFunc}
    hasMore={true || false}
    loader={<div className="loader" key={0}>Loading ...</div>}
>
    {items} // <-- This is the content you want to load
</InfiniteScroll>
```

### DOM scroll events

```js
<div style="height:700px;overflow:auto;">
    <InfiniteScroll
        pageStart={0}
        loadMore={loadFunc}
        hasMore={true || false}
        loader={<div className="loader" key={0}>Loading ...</div>}
        useWindow={false}
    >
        {items}
    </InfiniteScroll>
</div>
```

### Custom parent element

You can define a custom `parentNode` element to base the scroll calulations on.

```js
<div style="height:700px;overflow:auto;" ref={(ref) => this.scrollParentRef = ref}>
    <div>
        <InfiniteScroll
            pageStart={0}
            loadMore={loadFunc}
            hasMore={true || false}
            loader={<div className="loader" key={0}>Loading ...</div>}
            useWindow={false}
            getScrollParent={() => this.scrollParentRef}
        >
            {items}
        </InfiniteScroll>
    </div>
</div>
```

## Props

| Name              | Required | Type         | Default   | Description                                                                                                                                                                         |
| :---------------- | :------- | :----------- | :-------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `children`        | Yes      | `Node`   |           | Anything that can be rendered (same as PropType's Node) |
| `loadMore`        | Yes      | `Function`   |           | A callback when more items are requested by the user. Receives a single parameter specifying the page to load e.g. `function handleLoadMore(page) { /* load more items here */ }` } |
| `element`         |          | `Component`  | `'div'`   | Name of the element that the component should render as.                                                                                                                            |
| `hasMore`         |          | `Boolean`    | `false`   | Whether there are more items to be loaded. Event listeners are removed if `false`.                                                                                                  |
| `initialLoad`     |          | `Boolean`    | `true`    | Whether the component should load the first set of items.                                                                                                                           |
| `isReverse`       |          | `Boolean`    | `false`   | Whether new items should be loaded when user scrolls to the top of the scrollable area.                                                                                             |
| `loader`          |          | `Component`  |           | A React component to render while more items are loading. The parent component must have a unique key prop.                                                                         |
| `pageStart`       |          | `Number`     | `0`       | The number of the first page to load, With the default of `0`, the first page is `1`.                                                                                               |
| `getScrollParent` |          | `Function`   |           | Override method to return a different scroll listener if it's not the immediate parent of InfiniteScroll.                                                                           |
| `threshold`       |          | `Number`     | `250`     | The distance in pixels before the end of the items that will trigger a call to `loadMore`.                                                                                          |
| `useCapture`      |          | `Boolean`    | `false`   | Proxy to the `useCapture` option of the added event listeners.                                                                                                                      |
| `useWindow`       |          | `Boolean`    | `true`    | Add scroll listeners to the window, or else, the component's `parentNode`.                                                                                                          |

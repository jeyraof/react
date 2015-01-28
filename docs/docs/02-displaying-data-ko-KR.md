---
id: displaying-data-ko-KR
title: 데이터를 표시하기
permalink: displaying-data-ko-KR.html
prev: why-react-ko-KR.html
next: jsx-in-depth-ko-KR.html
---

UI를 가지고 할 수 있는 가장 기초적인 것은 데이터를 표시하는 것입니다. React는 데이터를 표시하고 데이터가 변할 때마다 인터페이스를 최신의 상태로 자동으로 유지하기 쉽게 해 줍니다.

## 시작하기

정말 간단한 예제를 보도록 하죠. 다음과 같은 코드의 `hello-react.html` 파일을 만듭시다.

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Hello React</title>
    <script src="http://fb.me/react-{{site.react_version}}.js"></script>
    <script src="http://fb.me/JSXTransformer-{{site.react_version}}.js"></script>
  </head>
  <body>
    <div id="example"></div>
    <script type="text/jsx">

      // ** 코드는 여기에 작성하면 됩니다! **

    </script>
  </body>
</html>
```

나머지의 문서에서, 우리는 자바스크립트 코드에만 집중하고 그 코드가 위와 같은 HTML 템플릿에 들어갔다고 가정할 것입니다. 위의 주석 부분을 다음과 같은 자바스크립트 코드로 바꿔 보세요:

```javascript
var HelloWorld = React.createClass({
  render: function() {
    return (
      <p>
        안녕, <input type="text" placeholder="이름을 여기에 작성하세요" />!
        지금 시간은 {this.props.date.toTimeString()} 이야.
      </p>
    );
  }
});

setInterval(function() {
  React.render(
    <HelloWorld date={new Date()} />,
    document.getElementById('example')
  );
}, 500);
```


## 반응적(Reactive) 갱신

in a web browser and type your name into the text field. Notice that React is only changing the time string in the UI — any input you put in the text field remains, even though you haven't written any code to manage this behavior. React figures it out for you and does the right thing.
`hello-react.html` 파일을 웹 브라우저에서 열어 당신의 이름을 텍스트 필드에 써 보세요. 리액트는 단지 시간을 표시하는 부분만을 바꿉니다 — 텍스트 필드 안에 입력산 것은 그대로 있구요, 당신이 이 동작을 관리하는 그 어떤 코드도 쓰지 않았음에도 불구하고 말이죠.


The way we are able to figure this out is that React does not manipulate the DOM unless it needs to. **It uses a fast, internal mock DOM to perform diffs and computes the most efficient DOM mutation for you.**
우리가 이걸 할 수 있었던 건 리액트는 필요하지 않은 경우 DOM을 업데이트하지 않기 때문잊니다. React는 빠른 내부의 돔 모형을 이용하여 변경된 부분을 측정하고, 가장 효율적인 DOM 변경 방법을 계산해 줍니다.

The inputs to this component are called `props` — short for "properties". They're passed as attributes in JSX syntax. You should think of these as immutable within the component, that is, **never write to `this.props`**.


## Components are Just Like Functions

React components are very simple. You can think of them as simple functions that take in `props` and `state` (discussed later) and render HTML. Because they're so simple, it makes them very easy to reason about.

> Note:
>
> **One limitation**: React components can only render a single root node. If you want to return multiple nodes they *must* be wrapped in a single root.


## JSX Syntax

We strongly believe that components are the right way to separate concerns rather than "templates" and "display logic." We think that markup and the code that generates it are intimately tied together. Additionally, display logic is often very complex and using template languages to express it becomes cumbersome.

We've found that the best solution for this problem is to generate HTML and component trees directly from the JavaScript code such that you can use all of the expressive power of a real programming language to build UIs.

In order to make this easier, we've added a very simple, **optional** HTML-like syntax to create these React tree nodes.

**JSX lets you create JavaScript objects using HTML syntax.** To generate a link in React using pure JavaScript you'd write:

`React.createElement('a', {href: 'http://facebook.github.io/react/'}, 'Hello!')`

With JSX this becomes:

`<a href="http://facebook.github.io/react/">Hello!</a>`

We've found this has made building React apps easier and designers tend to prefer the syntax, but everyone has their own workflow, so **JSX is not required to use React.**

JSX is very small. To learn more about it, see [JSX in depth](/react/docs/jsx-in-depth.html). Or see the transform in action in [our live JSX compiler](/react/jsx-compiler.html).

JSX is similar to HTML, but not exactly the same. See [JSX gotchas](/react/docs/jsx-gotchas.html) for some key differences.

The easiest way to get started with JSX is to use the in-browser `JSXTransformer`. We strongly recommend that you don't use this in production. You can precompile your code using our command-line [react-tools](http://npmjs.org/package/react-tools) package.


## React without JSX

JSX is completely optional. You don't have to use JSX with React. You can create these trees through `React.createElement`. The first argument is the tag, pass a properties object as the second argument and children to the third argument.

```javascript
var child = React.createElement('li', null, 'Text Content');
var root = React.createElement('ul', { className: 'my-list' }, child);
React.render(root, document.body);
```

As a convenience you can create short-hand factory functions to create elements from custom components.

```javascript
var Factory = React.createFactory(ComponentClass);
...
var root = Factory({ custom: 'prop' });
React.render(root, document.body);
```

React already has built-in factories for common HTML tags:

```javascript
var root = React.DOM.ul({ className: 'my-list' },
             React.DOM.li(null, 'Text Content')
           );
```

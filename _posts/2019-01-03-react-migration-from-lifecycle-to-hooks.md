---
layout: default
title:  React migration from lifecycle to hooks
date:   2019-01-03
permalink: /react-migration-from-lifecycle-to-hooks/
cover_url: /assets/image/react-hooks.png
comments: true
---

If you have ever used React, you should already be familiar with lifecycles.
Whether you like it or love it, React hooks are going to change the way we use them.

If you are curious, here is the [motivation for React hooks](https://reactjs.org/docs/hooks-intro.html#motivation). In this post I am going to show you how to convert lifecycles class methods into react hooks.

## componentDidMount

```javascript
class Example extends React.Component {
  componentDidMount() {
    console.log('I am mounted!');
  }
  render() {
    return null;
  }
}
```

```javascript
function Example() {
  useEffect(() => console.log('mounted'), []);
  return null;
}
```

## componentDidMount and componentDidUpdate

```javascript
componentDidMount() {
  console.log('mounted or updated');
}

componentDidUpdate() {
  console.log('mounted or updated');
}
```

```javascript
useEffect(() => console.log('mounted or updated'));
```

## componentWillUnmount
```javascript
componentWillUnmount() {
  console.log('will unmount');
}
```

```javascript
useEffect(() => {
  return () => {
    console.log('will unmount');
  }
}, []);
```

## shouldComponentUpdate
```
class Example extends React.Component {
  shouldComponentUpdate(nextProps) {
    return !(this.props.first === nextProps.first && this.props.last === nextProps.last);
  }

  render() {
    return <span>{this.props.first} {this.props.last}</span>;
  }
}
```

```
function ExamplePure(props) {
  return <span>{this.props.first} {this.props.last}</span>;
}

function propsAreEqual() {
  return this.props.first === nextProps.first && this.props.last === nextProps.last;
}

const Example = React.memo(ExamplePure, propsAreEqual);
```

```
function ExamplePure(props) {
  return <span>{this.props.first} {this.props.last}</span>;
}

const Example = React.memo(ExamplePure);
```

---

## Reference:
https://reactjs.org/docs/hooks-faq.html#from-classes-to-hooks

## TODO: add my react hooks blog to this list
https://github.com/rehooks/awesome-react-hooks

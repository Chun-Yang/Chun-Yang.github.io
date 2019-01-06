---
layout: default
title:  Replace lifecycle with hooks in React
date:   2019-01-03
permalink: /replace-react-lifecycles-with-hooks/
cover_url: /assets/image/react-hooks.png
comments: true
---

If you have ever used React, you should be familiar with power of React lifecycles. The upcoming React hooks are about to change the way we handle lifecycles.

React hooks are a unification of existing features including state and lifecycles. In this post I am going to show you how to convert lifecycle class methods into React hooks to shine some light on React hooks.

For each of the three most common lifecycle methods (componentDidMount, componentDidUpdate, componentWillUnmount), I will demonstrate a class style implementation and a hooks style counterpart followed by an explanation.

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
[useEffect](https://reactjs.org/docs/hooks-reference.html#useeffect) is a React hook where you can apply side effects, for example, getting data from server.

The first argument is a callback that will be fired __after__ browser layout and paint. Therefore it does not block the painting process of the browser.

The second argument is an array of values (usually props).
- If any of the value in the array changes, the callback will be fired after every render.
- When it's not present, the callback will always be fired after every render.
- When it's an empty list, the callback will only be fired once, similar to componentDidMount.

## componentDidUpdate
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
There is not a straight forward implementation in hooks to replace componentDidUpdate. The `useEffect` function can be used to trigger callbacks after every render of the component including after component mounts and component updates.

However this is not a big problem since most of the time we place similar functions in componentDidMount and componentDidUpdate.

Mimicing only componentDidUpdate can be a discussion of another post.

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
When you return a function in the callback passed to `useEffect`, the returned function will be called before the component is removed from the UI.

As we discussed previously, we need to pass an empty list as the second argument for `useEffect` so that the callback will only be called once. This apply to the returned function too.

Normally we do cleanups in the componentWillUnmount. Let's say you want to create an event listener on componentDidMount and clean it up on componentDidUnmount. With hooks the code will be combined into one callback function.

We can create multiple hooks for different side effects and reuse them. Grouping correlated code together and making state management reusable is one of the main purpose of React hooks.

## useEffect vs useLayoutEffect
Now we can convert componentDidMount, componentDidUpdate, and componentWillUnmount into React hooks, great!

Not so fast, there is a catch: the effects are not exactly the same between the two styles.

> Unlike componentDidMount and componentDidUpdate, the function passed to useEffect fires after layout and paint, during a deferred event.

Normally this is not a problem. But if you want to manipulate DOM in the effect, and want to make sure it happens before browser paint, you need to use [useLayoutEffect](https://reactjs.org/docs/hooks-reference.html#uselayouteffect). The syntax is the same as `useEffect`.

## Summary
To sum it up, we can use `useEffect` hook to replace lifecycle methods, but they are not exactly the same. Try to think in hooks when you use them!

## References
- https://reactjs.org/docs/hooks-faq.html#from-classes-to-hooks
- https://reactjs.org/docs/hooks-reference.html#useeffect

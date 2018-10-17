# Fragments 

When you need to group the list of child element on one component. 
```js
render() {
  return (
    <React.Fragment>
      <ChildA />
      <ChildB />
      <ChildC />
    </React.Fragment>
  );
}
```
short syntax
```js
render() {
  return (
    <>
      <ChildA />
      <ChildB />
      <ChildC />
    <>
  );
}
```

ref : [https://reactjs.org/docs/fragments.html](https://reactjs.org/docs/fragments.html) 

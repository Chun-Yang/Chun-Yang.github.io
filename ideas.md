- replace shouldComponentUpdate with react hooks
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

- a cheat sheet to replace class style features with react hooks

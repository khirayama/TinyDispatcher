# TinyDispather
simple &amp; tiny event dispatcher for es6

### Getting Started

```
import TinyDispatcher from 'TinyDispatcehr';

let ApplicationDispatcher = new TinyDispatcher();
```

## API
It has 3 API(on, off, dispatch) only.

### on

```
const CHANGE_EVENT = 'CHANGE_EVENT';

ApplicationDispatcher.on(CHANGE_EVENT, callbak);
```

### off

```
const CHANGE_EVENT = 'CHANGE_EVENT';

ApplicationDispatcher.off(CHANGE_EVENT);
```

### dispatch

```
const CHANGE_EVENT = 'CHANGE_EVENT';
let payload = {
  message: 'Hello TinyDispatcher!'
};

ApplicationDispatcher.dispatch(CHANGE_EVENT, payload});
```

## example

### simple and complete example.

```
let CHANGE_EVENT = 'CHANGE_EVENT';

ApplicationDispatcher.on(CHANGE_EVENT, (payload) => {
  alert(payload.message);
});

setTimeout(() => {
  ApplicationDispatcher.dispatch(CHANGE_EVENT, {message: 'Hello TinyDispatcher!'}});
}, 1000);
```

### example in Flux Store.
```
import TinyDispatcher from 'TinyDispatcehr';

const CHANGE_EVENT = 'CHANGE';

class Store extends EventDispatcher {
  constructor() {
    super();
  }
  dispatchChange() {
    this.dispatch(CHANGE_EVENT);
  }
  addChangeListener(callback) {
    this.on(CHANGE_EVENT, callback);
  }
  removeChangeListener(callback) {
    this.removeListener(CHANGE_EVENT, callback);
  }
}

class SomeStore extends Store {
  constructor() {
    super();
    this._message = '';
  }
  _create(message) {
    this._message = message;
    this.dispatchChange(); // define Store extened TinyDispatcher.
  }
  getMessage() {
    return this._message;
  }
}
new SomeStore(); // singleton
```

### if you use React....
Linten Store's events at ```componentDisMount```.
```
class SomeComponent extends React.Component {
  constructor() {
    super();
    this.state = {
      message: 'Hello World.'
    };
  }
  componentDidMount() {
    SomeStore.addChangeListener(this._onChange.bind(this));
  }
  render() {
    return <div>{this.state.message}</div>;
  }
  _onChange() {
    this.setState({
      message: SomeStore.getMessage()
    });
  }
}
```

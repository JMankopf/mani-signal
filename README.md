# mani-signal
a simple and very fast signal class

## Build

```
$ npm install
$ npm run build
```
## Test

```
$ npm run test
```
## Usage
```
$ npm install mani-signal --save
```

#### without parameter
```typescript
import {Signal} from 'mani-signal';

const signal = new Signal();

signal.add(()=> {
    console.log('signal callback');
});

signal.dispatch();
```
#### with parameter
```typescript
import {Signal} from 'mani-signal';

const signal = new Signal<string>();

signal.add(param => {
    console.log(`signal callback with ${param}`);
});

signal.dispatch('hello world');
```
#### listen once
```typescript
import {Signal} from 'mani-signal';

const signal = new Signal();

signal.addOnce(() => {
    console.log(`will be called once`);
});

signal.dispatch();
signal.dispatch();

```
#### detach listener

```typescript
import {Signal} from 'mani-signal';

const signal = new Signal();

const binding = signal.add(() => {
    console.log(`won't be called`);
});

binding.detach();

signal.dispatch();
```

#### detach all

```typescript
import {Signal} from 'mani-signal';

const signal = new Signal();

signal.add(() => {
    console.log(`won't be called`);
});
signal.add(() => {
    console.log(`won't be called`);
});

signal.detachAll();

signal.dispatch();
```


#### with context

```typescript
import {Signal} from 'mani-signal';

class Foo {
    value = 'Bar';

    constructor() {
        const signal = new Signal();

        // pass the context as second parameter
        signal.add(this.handler, this);

        signal.dispatch();
    }

    handler() {
        // accessing 'this' within a callback
        console.log(this.value);
    }

}
```
#### deactivate/activate binding

```typescript
import {Signal} from 'mani-signal';

const signal = new Signal();

const binding = signal.add(() => {});

signal.dispatch(); // handler will be called

binding.setActive(false);

signal.dispatch(); // handler will not be called
```

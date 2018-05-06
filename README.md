# truffle-assertions

[![npm version](https://badge.fury.io/js/truffle-assertions.svg)](https://www.npmjs.com/package/truffle-assertions)
[![npm](https://img.shields.io/npm/dt/truffle-assertions.svg)](https://www.npmjs.com/package/truffle-assertions)
[![npm](https://img.shields.io/npm/l/truffle-assertions.svg)](https://www.npmjs.com/package/truffle-assertions)

This package adds additional assertions that can be used to test Ethereum smart contracts inside Truffle tests.

## Installation
truffle-assertions can be installed through npm:
```bash
npm install truffle-assertions
```

## Usage
To use this package, import it at the top of the Truffle test file:
```javascript
const truffleAssert = require('truffle-assertions');
```

## Assertions

### truffleAssert.eventEmitted(result, eventType, filter, message)
The `eventEmitted` assertion checks that an event with type eventType has been emitted by the transaction with result result. A filter function can be passed along to further specify requirements for the event arguments:

```javascript
truffleAssert.eventEmitted(result, 'TestEvent', (ev) => {
    return ev.param1 === 10 && ev.param2 === ev.param3;
});
```

When the filter parameter is omitted or set to null, the assertion checks just for event type:

```javascript
truffleAssert.eventEmitted(result, 'TestEvent');
```

Optionally, a custom message can be passed to the assertion, which will be displayed alongside the default one:

```javascript
truffleAssert.eventEmitted(result, 'TestEvent', (ev) => {
    return ev.param1 === 10 && ev.param2 === ev.param3;
}, 'TestEvent should be emitted with correct parameters');
```

The default messages are
```javascript
`Event of type ${eventType} was not emitted`
`Event filter for ${eventType} returned no results`
```
Depending on the reason for the assertion failure.

### truffleAssert.eventNotEmitted(result, eventType, filter, message)
The `eventNotEmitted` assertion checks that an event with type eventType has not been emitted by the transaction with result result. A filter function can be passed along to further specify requirements for the event arguments:

```javascript
truffleAssert.eventNotEmitted(result, 'TestEvent', (ev) => {
    return ev.param1 === 10 && ev.param2 === ev.param3;
});
```

When the filter parameter is omitted or set to null, the assertion checks just for event type:

```javascript
truffleAssert.eventNotEmitted(result, 'TestEvent');
```

Optionally, a custom message can be passed to the assertion, which will be displayed alongside the default one:

```javascript
truffleAssert.eventNotEmitted(result, 'TestEvent', null, 'TestEvent should not be emitted');
```

The default messages are
```javascript
`Event of type ${eventType} was emitted`
`Event filter for ${eventType} returned results`
```
Depending on the reason for the assertion failure.

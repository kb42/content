---
title: Promise.prototype.finally()
short-title: finally()
slug: Web/JavaScript/Reference/Global_Objects/Promise/finally
page-type: javascript-instance-method
browser-compat: javascript.builtins.Promise.finally
sidebar: jsref
---

The **`finally()`** method of {{jsxref("Promise")}} instances schedules a function to be called when the promise is settled (either fulfilled or rejected). It immediately returns another {{jsxref("Promise")}} object, allowing you to [chain](/en-US/docs/Web/JavaScript/Guide/Using_promises#chaining) calls to other promise methods.

This lets you avoid duplicating code in both the promise's {{jsxref("Promise/then", "then()")}} and {{jsxref("Promise/catch", "catch()")}} handlers.

{{InteractiveExample("JavaScript Demo: Promise.prototype.finally()", "taller")}}

```js interactive-example
function checkMail() {
  return new Promise((resolve, reject) => {
    if (Math.random() > 0.5) {
      resolve("Mail has arrived");
    } else {
      reject(new Error("Failed to arrive"));
    }
  });
}

checkMail()
  .then((mail) => {
    console.log(mail);
  })
  .catch((err) => {
    console.error(err);
  })
  .finally(() => {
    console.log("Experiment completed");
  });
```

## Syntax

```js-nolint
promiseInstance.finally(onFinally)
```

### Parameters

- `onFinally`
  - : A function to asynchronously execute when this promise becomes settled. Its return value is ignored unless the returned value is a rejected promise. The function is called with no arguments.

### Return value

Returns a new {{jsxref("Promise")}} immediately. This new promise is always pending when returned, regardless of the current promise's status. If `onFinally` throws an error or returns a rejected promise, the new promise will reject with that value. Otherwise, the new promise will settle with the same state as the current promise.

## Description

The `finally()` method can be useful if you want to do some processing or cleanup once the promise is settled, regardless of its outcome.

The `finally()` method is very similar to calling {{jsxref("Promise/then", "then(onFinally, onFinally)")}}. However, there are a couple of differences:

- When creating a function inline, you can pass it once, instead of being forced to either declare it twice, or create a variable for it.
- The `onFinally` callback does not receive any argument. This use case is for precisely when you _do not care_ about the rejection reason or the fulfillment value, and so there's no need to provide it.
- A `finally()` call is usually transparent and reflects the eventual state of the original promise. So for example:
  - Unlike `Promise.resolve(2).then(() => 77, () => {})`, which returns a promise eventually fulfilled with the value `77`, `Promise.resolve(2).finally(() => 77)` returns a promise eventually fulfilled with the value `2`.
  - Similarly, unlike `Promise.reject(3).then(() => {}, () => 88)`, which returns a promise eventually fulfilled with the value `88`, `Promise.reject(3).finally(() => 88)` returns a promise eventually rejected with the reason `3`.

> [!NOTE]
> A `throw` (or returning a rejected promise) in the `finally` callback still rejects the returned promise. For example, both `Promise.reject(3).finally(() => { throw 99; })` and `Promise.reject(3).finally(() => Promise.reject(99))` reject the returned promise with the reason `99`.

Like {{jsxref("Promise/catch", "catch()")}}, `finally()` internally calls the `then` method on the object upon which it was called. If `onFinally` is not a function, `then()` is called with `onFinally` as both arguments — which, for {{jsxref("Promise.prototype.then()")}}, means that no useful handler is attached. Otherwise, `then()` is called with two internally created functions, which behave like the following:

> [!WARNING]
> This is only for demonstration purposes and is not a polyfill.

```js
promise.then(
  (value) => Promise.resolve(onFinally()).then(() => value),
  (reason) =>
    Promise.resolve(onFinally()).then(() => {
      throw reason;
    }),
);
```

Because `finally()` calls `then()`, it supports subclassing. Moreover, notice the {{jsxref("Promise.resolve()")}} call above — in reality, `onFinally()`'s return value is resolved using the same algorithm as `Promise.resolve()`, but the actual constructor used to construct the resolved promise will be the subclass. `finally()` gets this constructor through [`promise.constructor[Symbol.species]`](/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/Symbol.species).

## Examples

### Using finally()

```js
let isLoading = true;

fetch(myRequest)
  .then((response) => {
    const contentType = response.headers.get("content-type");
    if (contentType && contentType.includes("application/json")) {
      return response.json();
    }
    throw new TypeError("Oops, we haven't got JSON!");
  })
  .then((json) => {
    /* process your JSON further */
  })
  .catch((error) => {
    console.error(error); // this line can also throw, e.g. when console = {}
  })
  .finally(() => {
    isLoading = false;
  });
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- [Polyfill of `Promise.prototype.finally` in `core-js`](https://github.com/zloirock/core-js#ecmascript-promise)
- [es-shims polyfill of `Promise.prototype.finally`](https://www.npmjs.com/package/promise.prototype.finally)
- {{jsxref("Promise")}}
- {{jsxref("Promise.prototype.then()")}}
- {{jsxref("Promise.prototype.catch()")}}

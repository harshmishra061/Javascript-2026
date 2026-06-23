```js
Function.prototype.myBind = function (context, ...presetArgs) {
    if (typeof this !== "function") {
        throw new TypeError(
            "myBind should be called on a function"
        );
    }

    const originalFn = this;

    function boundFn(...newArgs) {

        // true when called using new
        const isConstructor =
            this instanceof boundFn;

        const finalContext =
            isConstructor
                ? this
                : (context ?? globalThis);

        return originalFn.apply(
            finalContext,
            [...presetArgs, ...newArgs]
        );
    }

    return boundFn;
};
```

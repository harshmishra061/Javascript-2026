Implement a method flatten() on Array.prototype that:

Flattens a deeply nested array of any depth
Works on any array instance
Returns a new flat array
Does NOT modify the original array
```js
Array.prototype.fullFlatten = function() {
    let result = [];
    
    function helper(arr) {
        for(let item of arr) {
            if(Array.isArray(item)) {
                helper(item);
            } else {
                result.push(item);
            }
        }
    }
    
    helper(this);
    return result;
}
```

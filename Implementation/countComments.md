Problem: Count Total Comments in a Nested Thread

Implement a function countComments(comments) that calculates the total number of comments in a nested discussion thread.

Each comment can contain multiple replies, and replies themselves follow the exact same structure (recursive tree).

Your function should count:

The root comment
Every nested reply at any depth

Additionally:

Validation Rules
Throw an error if:
    a comment is malformed (text missing or replies missing)
    replies is not an array
    circular references are detected

```js
function countComments(comment, visited = new Set()) {
    if (
        !comment ||
        typeof comment !== "object" ||
        !("text" in comment) ||
        !("replies" in comment) ||
        !Array.isArray(comment.replies)
    ) {
        throw new Error("Invalid comment structure");
    }

    if (visited.has(comment)) {
        throw new Error("Circular reference found");
    }

    visited.add(comment);

    let count = 1;

    for (const reply of comment.replies) {
        count += countComments(reply, visited);
    }

    return count;
}
```

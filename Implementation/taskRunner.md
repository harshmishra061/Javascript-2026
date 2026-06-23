Problem: Implement a Concurrent Task Runner

Create a TaskRunner class that executes asynchronous tasks while enforcing a maximum concurrency limit.

At any time:

Maximum concurrency tasks can run simultaneously.
Additional tasks should wait in a queue.
Once a running task completes, the next waiting task should begin automatically.

```js
class TaskRunner {
    constructor(concurrency) {
        this.maxConcurrency = concurrency;
        this.currConcurrency = 0;
        this.queue = [];
    }

    push(task) {
        this.queue.push(task);
        this.execute();
    }

    execute() {
        // Fill all available slots
        while (
            this.currConcurrency < this.maxConcurrency &&
            this.queue.length > 0
        ) {
            const task = this.queue.shift();

            this.currConcurrency++;

            // Start task WITHOUT blocking the loop
            Promise.resolve()
                .then(task)
                .catch(() => {
                    // handle task failure safely (optional)
                })
                .finally(() => {
                    this.currConcurrency--;
                    this.execute(); // try scheduling next task
                });
        }
    }
}
```

# Promise Chain in Javascript

Ever wanted to do something like this:

    obj1.chain().func1('foo').func2('bar').then(function (result) {
        // Do something
    });

where func1 and func2 are asynchronous functions on obj1 and where you want to execute func2 after func1 is done?

This is now possible!

Look at the examples to get started.

This code simulates blocking calls in Javascript using native Promises.

Only supports functions that return Promise objects.

## How it works

When the `chain` function is called on an object or class, it generates a promise chain object where the functions specified in `chainable` are mocked. When these functions are called, the function name and the given arguments are put into a queue. When the `then` function is called, these function names and arguments are pulled from the queue and executed after the previous one has resolved. After every function in the queue is finished and no error has occured, the callback in the `then` function is called with the result of the promise of the last function in the queue. This `then` function also returns a regular Promise object that you can use to call `then` again or call `catch`. After the promise chain is done and before the callback and resolve are called, the queue gets cleared and the queuePointer gets reset.

To give the functionality to an object or class, give the object or class the `chain` function given in the examples, and give the object or class a `chainable` member, which is an array with the names of the functions that support chaining. A function supports chaining if it always returns a Promise object.

## Examples

* poc1.html shows regular usage of promise chains, 1 object is given the functionality.  
* poc2.html shows how you can give multiple objects the functionality and how you can have multiple promise chains running at the same time.

## License

You may do anything with the code in this repository, but you must link back to this repository, either in code comment or in documentation.

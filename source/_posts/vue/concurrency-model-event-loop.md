---
title: Concurrency Model and The Event Loop
date: 2022-1-10 11:23:50
categories: 
- vue
tags:
---

JavaScript has a concurrency model based on an event loop, which is responsible for executing the code, collecting and processing events, and executing queued sub-tasks.This model is quite different from models in other languages like C and Java.



### Run Time Concepts



![Stack, heap, queue](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop/the_javascript_runtime_environment_example.svg)

### [Stack](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#stack)

Function calls form a stack of *frames*.

```
function foo(b) {
  let a = 10
  return a + b + 11
}

function bar(x) {
  let y = 3
  return foo(x * y)
}

const baz = bar(7) // assigns 42 to baz
```

Copy to Clipboard

Order of operations:

1. When calling `bar`, a first frame is created containing references to `bar`'s arguments and local variables.
2. When `bar` calls `foo`, a second frame is created and pushed on top of the first one, containing references to `foo`'s arguments and local variables.
3. When `foo` returns, the top frame element is popped out of the stack (leaving only `bar`'s call frame).
4. When `bar` returns, the stack is empty.

Note that the arguments and local variables may continue to exist, as they are stored outside the stack — so they can be accessed by any [nested functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions#nested_functions_and_closures) long after their outer function has returned

### [Heap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#heap)

Objects are allocated in a heap which is just a name to denote a large (mostly unstructured) region of memory.

### [Queue](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#queue)

A JavaScript runtime uses a message queue, which is a list of messages to be processed. Each message has an associated function that gets called to handle the message.

At some point during the [event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#event_loop), the runtime starts handling the messages on the queue, starting with the oldest one. To do so, the message is removed from the queue and its corresponding function is called with the message as an input parameter. As always, calling a function creates a new stack frame for that function's use.

The processing of functions continues until the stack is once again empty. Then, the event loop will process the next message in the queue (if there is one),so some of event loop's task is clear queue & stack.



## [Event loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#event_loop)

The **event loop** got its name because of how it's usually implemented, which usually resembles:

```
while (queue.waitForMessage()) {
  queue.processNextMessage()
}
```

Copy to Clipboard

`queue.waitForMessage()` waits synchronously for a message to arrive (if one is not already available and waiting to be handled).

### ["Run-to-completion"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#run-to-completion)

Each message is processed completely before any other message is processed.

This offers some nice properties when reasoning about your program, including the fact that whenever a function runs, it cannot be pre-empted and will run entirely before any other code runs (and can modify data the function manipulates). This differs from C, for instance, where if a function runs in a thread, it may be stopped at any point by the runtime system to run some other code in another thread.

A downside of this model is that if a message takes too long to complete, the web application is unable to process user interactions like click or scroll. The browser mitigates this with the "a script is taking too long to run" dialog. A good practice to follow is to make message processing short and if possible cut down one message into several messages.



### [Adding messages](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#adding_messages)

In web browsers, messages are added anytime an event occurs and there is an event listener attached to it. If there is no listener, the event is lost. So a click on an element with a click event handler will add a message—likewise with any other event.

### [Several runtimes communicating together](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#several_runtimes_communicating_together)

A web worker or a cross-origin `iframe` has its own stack, heap, and message queue. Two distinct runtimes can only communicate through sending messages via the [`postMessage`](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage) method. This method adds a message to the other runtime if the latter listens to `message` events.

## [Never blocking](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#never_blocking)

A very interesting property of the event loop model is that JavaScript, unlike a lot of other languages, never blocks. Handling I/O is typically performed via events and callbacks, so when the application is waiting for an [IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API) query to return or an [XHR](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) request to return, it can still process other things like user input.



Ref:https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop

## What is RXJS
  - RxJS is a library for composing asynchronous and event-based programs by using observable sequences. 
  - It provides one core type, the <b>Observable, satellite types (Observer, Schedulers, Subjects)</b> and <b>operators inspired by Array methods (map, filter, reduce, every, etc)</b> to allow handling asynchronous events as collections.
  
  
  
  
  
<b>Observable:</b> represents the idea of an invokable collection of future values or events.
  
<b>Observer:</b> is a collection of callbacks that knows how to listen to values delivered by the Observable.
  
<b>Subscription:</b> represents the execution of an Observable, is primarily useful for cancelling the execution.
  
<b>Operators:</b> are pure functions that enable a functional programming style of dealing with collections with operations like map, filter, concat, reduce, etc.
  
<b>Subject:</b> is equivalent to an EventEmitter, and the only way of multicasting a value or event to multiple Observers.
  
<b>Schedulers:</b> are centralized dispatchers to control concurrency, allowing us to coordinate when computation happens on e.g. setTimeout or requestAnimationFrame or others.

* help us continues data streame
## Observables
 * observables emit data over a preiod of time.

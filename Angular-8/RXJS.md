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
 * Emits multiple values over a period of time.
 * Observables are lazy Push collections of multiple values.
 * Lazy. An observable is not called until we subscribe to the observable
 * Observable provides operators like map, forEach, filter, reduce, retry, retryWhen etc.

## pull and push 
PULL | PUSH 
--- | --- | 
Pull	Passive: produces data when requested. | Push	Active: produces data at its own pace.	
Active: decides when data is requested. | Passive: reacts to received data.

## Operators

### Combination
* combineAll
* combineLatest - When any observable emits a value, emit the last emitted value from each.
  - emit latest value from each observable
  - [link](https://www.learnrxjs.io/learn-rxjs/operators/combination/combinelatest)
```
  let firstTimer$ = interval(1000).pipe(take(10),map(x=> x+10));
    let secondTimer$ = interval(3000).pipe(take(10),map(y=> y+20));
    let combined = combineLatest(firstTimer$, secondTimer$);
    combined.subscribe((data) => {
      console.log(data);
    });
```
output
```
[12,20]
[13,20]....

```

* concat
* concatAll
* endWith
* forkJoin
* merge 
* mergeAll
* pairwise
* race
* startWith
* withLatestFrom 
* zip
### Conditional
* defaultIfEmpty
* every
* iif
* sequenceequal
## Creation
* ajax
* create
* defer
* empty
* from
* fromEvent
* generate
* interval
* of 
* range
* throw
* timer
## Error Handling
* catch / catchError 
* retry
* retryWhen
## Filtering
* audit
* auditTime
* debounce
* debounceTime
* distinct
* distinctUntilChanged 
* distinctUntilKeyChanged
* filter 
* find
* first
* ignoreElements
* last
* sample
* single
* skip
* skipUntil
* skipWhile
* take ⭐
* takeLast
* takeUntil ⭐
* takeWhile
* throttle
* throttleTime
## Multicasting
* multicast
* publish
* share ⭐
* shareReplay ⭐
## Transformation
* buffer
* bufferCount
* bufferTime ⭐
* bufferToggle
* bufferWhen
* concatMap ⭐
* concatMapTo
* expand
* exhaustMap
* groupBy
* map ⭐
* mapTo
* mergeMap / flatMap ⭐
* mergeScan
* partition
* pluck
* reduce
* scan ⭐
* switchMap ⭐
* switchMapTo
* toArray
* window
* windowCount
* windowTime
* windowToggle
* windowWhen
## Utility
* tap / do ⭐
* delay
* delayWhen
* dematerialize
* finalize / finally
* let
* repeat
* repeatWhen
* timeInterval
* timeout
* timeoutWith
* toPromise

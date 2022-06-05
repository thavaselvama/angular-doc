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
* combineLatest ⭐ - When any observable emits a value, emit the last emitted value from each.
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

* concat ⭐ - Subscribe to observables in order as previous completes
  - one observable complete then should start second one
```
 let firstTimer$ = interval(1000).pipe(take(5),map(x=> x+10));
    let secondTimer$ = interval(3000).pipe(take(10),map(y=> y+20));
    let combined = concat(firstTimer$, secondTimer$);
    combined.subscribe((data) => {
      console.log(data);
    });
```

output
```
10,
11,
12,
13,
14,
15, /// end first $
21,
22,23,24,25,..29
```

* concatAll
* endWith
* forkJoin - When all observables complete, emit the last emitted value from each.
```
 let firstTimer$ = interval(1000).pipe(take(5),map(x=> x+10));
    let secondTimer$ = interval(3000).pipe(take(10),map(y=> y+20));
    let combined = forkJoin(firstTimer$, secondTimer$);
    combined.subscribe((data) => {
      console.log(data);
    });
```

output 

```
[14,29]
```
* merge ⭐ - Turn multiple observables into a single observable.
   ```
    let firstTimer$ = interval(1000).pipe(take(5),map(x=> x+10));
    let secondTimer$ = interval(3000).pipe(take(10),map(y=> y+20));
    let combined = merge(firstTimer$, secondTimer$);
    combined.subscribe((data) => {
      console.log(data);
    });
   
   ```
 example:
 
 ```
10,
11,
12,
13,
14,
15,
20,21,....29
 ```
* mergeAll
* pairwise
* race - The observable to emit first is used.
        - if 2 observable which one first emit will give that one, second observable should not emit

example
```
 let firstTimer$ = interval(1000).pipe(take(5),map(x=> x+10));
    let secondTimer$ = interval(3000).pipe(take(10),map(y=> y+20));
    let combined = race(firstTimer$, secondTimer$);
    combined.subscribe((data) => {
      console.log(data);
    });

```
output
```
10,11,12,13,14
```

* startWith ⭐ - Emit given value first.
      - user define value first
      -  data$.pipe(startWith("js")
 example:
 
 ```
 let data$ = of("hello","react","node")
    data$.pipe(startWith("js"),
    scan((acc, curr) => `${acc} ${curr}`)
    ).subscribe(val => console.log(val))
 ```
 
 output:
 ```
 js hello,
 js react,
 js node
 
 ```
* withLatestFrom ⭐
* zip - After all observables emit, emit values as an array
     
 ```
  let num$ = of(1,2,3);
    let name$ = of('react','node','angular');
    let dev$ = of(true,true,false);

    zip(num$,name$,dev$).subscribe(data=>{
      console.log(data)
    })
 
 ````
output
```
[1,'react',true];
[2,'node',true]
[3,'angular',false]
 ```
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
* bufferTime ⭐ - Collect emitted values until provided time has passed, emit as array.

                 - if set time example 5 sec, with in 5 sec click multiple time, it will collect how many time click and give the array of data
    ```
     const source = fromEvent(document,'click')
    const example = source.pipe(bufferTime(5000));
    const subscribe = example.subscribe((val) =>
      console.log('Buffered with Time:', val)
    );
    ```
    output:
     []   /// without click
     
     ['Buffered with Time,'Buffered with Time'] // array value number of clicked
    
* bufferToggle
* bufferWhen
* concatMap ⭐ - Map values to inner observable, subscribe and emit in order.

                - collect all the mouse click and emit the value
                - first excute inner observable

```
output:
```
0,1,2,3 ---- one time clicked
0,1,2,3,0,1,2,3 --- two time clicked
```
const source = fromEvent(document,'click')
    const example = source.pipe(concatMap(ev => interval(1000).pipe(take(4))));
    const subscribe = example.subscribe((val) => 
      console.log('Buffered with Time:', val)
    );
    
  ```
* concatMapTo
* expand
* exhaustMap
* groupBy
* map ⭐
* mapTo
* mergeMap / flatMap ⭐ - merge 2 observable and excute 

                          - If the order of emission and subscription of inner observables 

```
const letters$ = of('a','b','c');

  let result$ = letters$
  .pipe(
   
    mergeMap(x=>interval(1000).pipe(map(i=> x+i),take(4)))
  )
  result$.subscribe(data=>{
    console.log(data)
  })
  
  ```
  
  output:
  ```
  a0,b0,c0,a1,b1,c1,a2,b2,c2,a3,b3,c3.
  
 ```
* mergeScan
* partition
* pluck
* reduce
* scan ⭐
* switchMap ⭐ - Map to observable, complete previous inner observable, emit values.
                 - excute the order, excution not complete inner observable, if comes new parent observable it will skip parent and inner observable.
 ```
  const letters$ = of('a','b','c');

  let result$ = letters$
  .pipe(
   
    switchMap(x=>interval(1000).pipe(map(i=> x+i),take(4)))
  )
  result$.subscribe(data=>{
    console.log(data)
  })
 ```
 
 output:
 
 c0,c1,c2,c3
 
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

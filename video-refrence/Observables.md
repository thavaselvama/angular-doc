
# Observables
- Angular makes use of observables as an interface to handle a variety of common asynchronous operations.
- Observables provide support for passing messages between publishers and subscribers in your application. 

- Its various data source usr input(event),http request
- data emitted by observable
- Emit data Observable using ```import { Observable } from 'rxjs'; ```
- subscribe function receive data from Observables ```this.source.subscribe(val => console.log(val)```
```
import { Observable } from 'rxjs';
```
```
import { Component } from '@angular/core';

import { from } from 'rxjs';
import { Observable } from 'rxjs';
import { timer } from 'rxjs';
@Component({
  selector: 'my-app',
   template: `<div><code>observable|async</code>:
       Time: {{ time | async }}</div>`,
  styleUrls: [ './app.component.css' ]
})

export class AppComponent {
  source  = timer(1000, 2000);
   subscribe = this.source.subscribe(val => console.log(val)
   );
  time = new Observable<string>(observer => {
    setInterval(() => observer.next(new Date().toString()), 1000);
  });
}
```
![](https://miro.medium.com/max/798/1*59J_8TUx-fYbhMuiY9R2JA.jpeg)

# Observer 

 -  its an <strong>subscribe()</strong>
### 1.Handle data 2. Handle error 3. Handle Completion

import packege ```import { Observer } from 'rxjs/Observer';```

```
const observable = Observable.create((obeserver : Observer)=>{
  setTimeout(()=>{
    obeserver.next("first")
  },2000)
})
observable.subscribe(
  (data : string)=>{
    console.log(data)
  }
)
```

- If implement observable one component, switch another component behind the screen observable implemented component destroy but observable subscription keep in memory.

- In this case should use unsubscribe(). import packege ```import { Subscription } from 'rxjs/Subscription';``

- this you can call ngOnDestroy Lifecycle hook.

Example :
```
import { Component, OnInit,OnDestroy } from '@angular/core';
import { Observable } from 'rxjs/Observable';
import { Observer } from 'rxjs/Observer';
import { Subscription } from 'rxjs/Subscription';
import 'rxjs/Rx';
@Component({
  selector: 'app-home',
  templateUrl: './home.component.html',
  styleUrls: ['./home.component.css']
})
export class HomeComponent implements OnInit,OnDestroy {
  numers : any = Subscription;
  mySubscription : any = Subscription;

  constructor() { }

  ngOnInit() {
    const number = Observable.interval(1000);
    this.numers = number.subscribe(
      (number: number) => {
        console.log( number)
      }
    )

    const observable = Observable.create((obeserver: Observer<string>) => {
      setTimeout(() => {
        obeserver.next("first")
      }, 2000)
    })
    this.mySubscription = observable.subscribe(
      (data: string) => {
        console.log(data)
      }
    )
  }
  ngOnDestroy(){
    this.numers.unsubscribe();
    this.mySubscription.unsubscribe()
  }

}

```
- navigate other component destroy 

```
ngOnDestroy(){
    this.numers.unsubscribe();
    this.mySubscription.unsubscribe()
  }

 ```
 
 ## Subject
 - event emitter you can communicate accross application,Observable and subscribe you can do at the time
 
 [link to Subject!](http://reactivex.io/documentation/subject.html)
 [link to Subject!](https://rxjs-dev.firebaseapp.com/guide/subject)
 
 - A Subject is like an Observable, but can multicast to many Observers. Subjects are like EventEmitters: they maintain a registry of many listeners.
```
import { Subject } from 'rxjs';
 
const subject = new Subject<number>();
 
subject.subscribe({
  next: (v) => console.log(`observerA: ${v}`)
});
subject.subscribe({
  next: (v) => console.log(`observerB: ${v}`)
});
 
subject.next(1);
subject.next(2);
 
// Logs:
// observerA: 1
// observerB: 1
// observerA: 2
// observerB: 2
```

Example subject

[link to Subject!](https://stackblitz.com/edit/vide0-observer?file=src%2Fapp%2Fapp.component.ts)
 




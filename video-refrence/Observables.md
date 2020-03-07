
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



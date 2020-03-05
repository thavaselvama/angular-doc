# User input
- User actions such as clicking a link, pushing a button, and entering text raise DOM events. This page explains how to bind those events to component event handlers using the Angular event binding syntax.

[link to User input!](https://stackblitz.com/angular/qrjjoaxddxa?file=src%2Fapp%2Fapp.component.html)

[Custom User input!](https://stackblitz.com/edit/cart-emit)

## Binding to user input events
 - You can use Angular event bindings to respond to any DOM event. Many DOM events are triggered by user input. Binding to these events provides a way to get input from the user.
```
<button (click)="onClickMe()">Click me!</button>
```
Ts file

```
@Component({
  selector: 'app-click-me',
  template: `
    <button (click)="onClickMe()">Click me!</button>
    {{clickMessage}}`
})
export class ClickMeComponent {
  clickMessage = '';

  onClickMe() {
    this.clickMessage = 'You are my hero!';
  }
}
```
## Get user input from the $event object
 - DOM events carry a payload of information that may be useful to the component. 
```
<input (keyup)="onKey($event)">
  <p>{{values}}</p>
  ```
  ```
  onKey(event: any) { // without type info
    this.values += event.target.value + ' | ';
  }
  ```
  ![Image of Yaktocat](https://angular.io/generated/images/guide/user-input/keyup1-anim.gif)
 
## Get user input from a template reference variable

There's another way to get the user data: use Angular [!template reference variables](https://angular.io/guide/template-syntax#ref-vars). These variables provide direct access to an element from within the template. To declare a template reference variable, precede an identifier with a hash (or pound) character (#).

```
@Component({
  selector: 'app-loop-back',
  template: `
    <input #box (keyup)="0">
    <p>{{box.value}}</p>
  `
})
export class LoopbackComponent { }
```
![image](https://angular.io/generated/images/guide/user-input/keyup-loop-back-anim.gif)

Another example

```
@Component({
  selector: 'app-key-up2',
  template: `
    <input #box (keyup)="onKey(box.value)">
    <p>{{values}}</p>
  `
})
export class KeyUpComponent_v2 {
  values = '';
  onKey(value: string) {
    this.values += value + ' | ';
  }
}
```
## Key event filtering (with key.enter)
 - The (keyup) event handler hears every keystroke.
 ```
 @Component({
  selector: 'app-key-up3',
  template: `
    <input #box (keyup.enter)="onEnter(box.value)">
    <p>{{value}}</p>
  `
})
export class KeyUpComponent_v3 {
  value = '';
  onEnter(value: string) { this.value = value; }
}
```
![](https://angular.io/generated/images/guide/user-input/keyup3-anim.gif)

## On blur
```
@Component({
  selector: 'app-key-up4',
  template: `
    <input #box
      (keyup.enter)="update(box.value)"
      (blur)="update(box.value)">

    <p>{{value}}</p>
  `
})
export class KeyUpComponent_v4 {
  value = '';
  update(value: string) { this.value = value; }
}
```

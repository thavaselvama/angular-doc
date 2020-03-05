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
  

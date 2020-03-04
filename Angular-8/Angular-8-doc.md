# Angular-8

# Template syntax

## Interpolation and Template Expressions
 - Interpolation allows you to incorporate calculated strings into the text between HTML element tags and within attribute assignments
   - In the following snippet, {{ currentCustomer }} is an example of interpolation.
 - Template expressions are what you use to calculate those strings.
   - template expression appears in quotes to the right of the = symbol as in [property]="expression"
   
 You can't use JavaScript expressions that have or promote side effects, including:

 - Assignments (=, +=, -=, ...)
- Operators such as new, typeof, instanceof, etc.
- Chaining expressions with ; or ,
- The increment and decrement operators ++ and --
- Some of the ES2015+ operators

- No support for the bitwise operators such as | and &
New template expression operators, such as |, ?. and !

## Expression context
- The expression context is typically the component instance. In the following snippets, the recommended within double curly braces and the itemImageUrl2 in quotes refer to properties of the AppComponent.

- example

```
<img [src]="itemImageUrl2">

```

##  HTML attribute vs. DOM property

- The distinction between an HTML attribute and a DOM property is key to understanding how Angular binding works. Attributes are defined by HTML. Properties are accessed from DOM (Document Object Model) nodes.

- Example

- When the browser renders 
```
<input id='name' type="text" value="Sarah">
```
- it creates a corresponding DOM node with a value property initialized to "Sarah".

```
var id. = document.getElementById('name');
console.log(id.getattribute('value')) /// Sarah
console.log(id.value) /// user enter value

```
# Property binding [property]
- Use property binding to set properties of target elements or directive @Input() decorators.
https://stackblitz.com/angular/dyraajpdmea?file=src%2Fapp%2Fapp.component.ts
## One-way in
-- One-way data binding will bind the data from the component to the view (DOM) or from view to the component. One-way data binding is unidirectional. You can only bind the data from component to the view or from view to the component.
```
import { Component } from "@angular/core";
@Component({
  selector: 'app-example',
  template: `
              <div>
              <strong>{{firstName}}</strong>
               <strong>{{lastName}}</strong>
              </div>
              `
})

export class AppComponent {
  firstName: string = "Yallaling";
  lastName:string = "Goudar";
}

```
- binding type
```
<!-- Notice the colSpan property is camel case -->
<tr><td [colSpan]="2">Span 2 columns</td></tr>
```
```
<button [disabled]="isUnchanged">Disabled Button</button>
<p [ngClass]="classes">[ngClass] binding to the classes property making this blue</p>
<img bind-src="itemImageUrl">
```
- Yet another is setting the model property of a custom component—a great way for parent and child components to communicate:

```
<app-item-detail [childItem]="parentItem"></app-item-detail>
```
## Attribute binding
- Set the value of an attribute directly with an attribute binding
```
<button [attr.aria-label]="actionName">{{actionName}} with Aria</button>
```
## Class binding
```
<h3>Basic specificity</h3>

<!-- The `class.special` binding will override any value for the `special` class in `classExpr`.  -->
<div [class.special]="isSpecial" [class]="classExpr">Some text.</div>

<!-- The `style.color` binding will override any value for the `color` property in `styleExpr`.  -->
<div [style.color]="color" [style]="styleExpr">Some text.</div>
```

## Event binding (event)
- Event binding allows you to listen for certain events such as keystrokes, mouse movements, clicks, and touches. For an example demonstrating all of the points in this section, see the 

https://angular.io/generated/live-examples/event-binding/stackblitz

![Image of Yaktocat](https://angular.io/generated/images/guide/template-syntax/syntax-diagram.svg)
```
<button (click)="onSave($event)">Save</button>
<button on-click="onSave($event)">on-click Save</button>
```
- Element events may be the more common targets, but Angular looks first to see if the name matches an event property of a known directive, as it does in the following example:

```
<h4>myClick is an event on the custom ClickDirective:</h4>
<button (myClick)="clickMessage=$event" clickable>click with myClick</button>
{{clickMessage}}
```
## Custom events with EventEmitter
- HTML
```
<img src="{{itemImageUrl}}" [style.display]="displayNone">
<span [style.text-decoration]="lineThrough">{{ item.name }}
</span>
<button (click)="delete()">Delete</button>
```
- ts 
```
// This component makes a request but it can't actually delete a hero.
@Output() deleteRequest = new EventEmitter<Item>();

delete() {
  this.deleteRequest.emit(this.item);
  this.displayNone = this.displayNone ? '' : 'none';
  this.lineThrough = this.lineThrough ? '' : 'line-through';
}
```

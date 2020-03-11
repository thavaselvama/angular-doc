# Angular-8
[Angular version History](https://medium.com/@lifenshades/difference-among-angular-8-7-6-5-4-3-2-breakdown-new-features-and-changes-811fb5f8e6f0)

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
```
<app-item-detail (deleteRequest)="deleteItem($event)" [item]="currentItem"></app-item-detail>
```

## Two-way binding [(...)]
- Two-way binding gives your app a way to share data between a component class and its template.
https://stackblitz.com/angular/oabeoendjyx?file=src%2Fapp%2Fapp.component.ts

### Basics of two-way binding
Two-way binding does two things:

  * Sets a specific element property.
  * Listens for an element change event.
  
## [(ngModel)]: Two-way binding
- The NgModel directive allows you to display a data property and update that property when the user makes changes. Here's an example:
```
<label for="example-ngModel">[(ngModel)]:</label>
<input [(ngModel)]="currentItem.name" id="example-ngModel">
```
```
<app-sizer [size]="fontSizePx" (sizeChange)="fontSizePx=$event"></app-sizer>
```
https://stackblitz.com/angular/kbelykomnrk?file=src%2Fapp%2Fapp.component.ts

### detailed example
```
<fieldset><h4>NgModel examples</h4>
  <p>Current item name: {{currentItem.name}}</p>
  <p>
    <label for="without">without NgModel:</label>
    <input [value]="currentItem.name" (input)="currentItem.name=$event.target.value" id="without">

  </p>

  <p>
    <label for="example-ngModel">[(ngModel)]:</label>
    <input [(ngModel)]="currentItem.name" id="example-ngModel">
  </p>

  <p>
    <label for="example-bindon">bindon-ngModel: </label>
    <input bindon-ngModel="currentItem.name" id="example-bindon">
  </p>

  <p>
    <label for="example-change">(ngModelChange)="...name=$event":</label>
    <input [ngModel]="currentItem.name" (ngModelChange)="currentItem.name=$event" id="example-change">
  </p>

  <p>
    <label for="example-uppercase">(ngModelChange)="setUppercaseName($event)"
      <input [ngModel]="currentItem.name" (ngModelChange)="setUppercaseName($event)" id="example-uppercase">
    </label>
  </p>
</fieldset>
```

## Template reference variables (#var)
- A template reference variable is often a reference to a DOM element within a template. It can also refer to a directive (which contains a component), an element, TemplateRef, or a web component.
```
<form #itemForm="ngForm" (ngSubmit)="onSubmit(itemForm)">
  <label for="name"
    >Name <input class="form-control" name="name" ngModel required />
  </label>
  <button type="submit">Submit</button>
</form>

<div [hidden]="!itemForm.form.valid">
  <p>{{ submitMessage }}</p>
</div>
```
https://stackblitz.com/angular/ryvkjqvabgj?file=src%2Fapp%2Fapp.component.ts

## @Input() and @Output() properties
- @Input() and @Output() allow Angular to share data between the parent context and child directives or components. An @Input() property is writable while an @Output() property is observable

### How to use @Input()

![image of Input](https://angular.io/generated/images/guide/inputs-outputs/input.svg)

### In the child
To use the @Input() decorator in a child component class, first import Input and then decorate the property with @Input():
```
import { Component, Input } from '@angular/core'; // First, import Input
export class ItemDetailComponent {
  @Input() item: string; // decorate the property with @Input()
}
```
### In the parent
```
<app-item-detail [item]="currentItem"></app-item-detail>
```
![image parent](https://angular.io/generated/images/guide/inputs-outputs/input-diagram-target-source.svg)


### How to use @Output()
- Use the @Output() decorator in the child component or directive to allow data to flow from the child out to the parent.
![output ](https://angular.io/generated/images/guide/inputs-outputs/output.svg)

### In the child
```
export class ItemOutputComponent {

  @Output() newItemEvent = new EventEmitter<string>();

  addNewItem(value: string) {
    this.newItemEvent.emit(value);
  }
}
```
### In the parent
```
export class AppComponent {
  items = ['item1', 'item2', 'item3', 'item4'];

  addItem(newItem: string) {
    this.items.push(newItem);
  }
}
```
### @Input() and @Output() together
![](https://angular.io/generated/images/guide/inputs-outputs/input-output-diagram.svg)

## The pipe operator (|)

```
<p>Title through uppercase pipe: {{title | uppercase}}</p>
<!-- convert title to uppercase, then to lowercase -->
<p>Title through a pipe chain: {{title | uppercase | lowercase}}</p>
<!-- pipe with configuration argument => "February 25, 1980" -->
<p>Manufacture date with date format pipe: {{item.manufactureDate | date:'longDate'}}</p>
<p>Item json pipe: {{item | json}}</p>

```
## Built-in template functions
### The $any() type cast function
 - Sometimes a binding expression triggers a type error during AOT compilation and it is not possible or difficult to fully specify the type. To silence the error, you can use the $any() cast function to cast the expression to the any type as in the following example:
 ```
 <p>The item's undeclared best by date is: {{$any(item).bestByDate}}</p>

 ```

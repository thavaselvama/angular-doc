reference [https://stackblitz.com/edit/thvangular8-input]

reference [https://stackblitz.com/angular/nqlorlypjek?file=src%2Fapp%2Fapp.component.ts]

https://angular.io/guide/inputs-outputs

## @Input() and @Output() properties

- @Input() and @Output() allow Angular to share data between the parent context and child directives or components. An @Input() property is writable while an @Output() property is observable

### Sending data to a child component
- The ```@Input()``` decorator in a child component or directive signifies that the property can receive its value from its parent component.

![image of Input](https://angular.io/generated/images/guide/inputs-outputs/input.svg)

<b>To use @Input(), you must configure the parent and child.</b>

### Configuring the child component
```
import { Component, Input } from '@angular/core'; // First, import Input
export class ItemDetailComponent {
  @Input() item: string; // decorate the property with @Input()
}

```
```
<p>
  Today's item: {{item}}
</p>
```
### Configuring the Parent component
 - The next step is to bind the property in the parent component's template.
```
 <app-item-detail [item]="currentItem"></app-item-detail>
```
```
export class AppComponent {
  currentItem = 'Television';
}
```
With @Input(), Angular passes the value for currentItem to the child so that item renders as Television.

The following diagram shows this structure:
![image of Input](https://angular.io/generated/images/guide/inputs-outputs/input-diagram-target-source.svg)

## Sending data to a parent component
The @Output() decorator in a child component or directive allows data to flow from the child to the parent.
![image of Input](https://angular.io/generated/images/guide/inputs-outputs/output.svg)

The child component uses the @Output() property to raise an event to notify the parent of the change. To raise an event, an @Output() must have the type of EventEmitter, which is a class in @angular/core that you use to emit custom events.

### Configuring the child component

```
import { Output, EventEmitter } from '@angular/core';
export class ItemOutputComponent {

  @Output() newItemEvent = new EventEmitter<string>();

  addNewItem(value: string) {
    this.newItemEvent.emit(value);
  }
}
```
### Configuring the child's template
```
<label>Add an item: <input #newItem></label>
<button (click)="addNewItem(newItem.value)">Add to parent's list</button>

```
### Configuring the parent component

```
export class AppComponent {
  items = ['item1', 'item2', 'item3', 'item4'];

  addItem(newItem: string) {
    this.items.push(newItem);
  }
}
```
### Configuring the parent's template
```
<app-item-output (newItemEvent)="addItem($event)"></app-item-output>

```
### Using @Input() and @Output() together
```
<app-input-output [item]="currentItem" (deleteRequest)="crossOffItem($event)"></app-input-output>
```
The target, item, which is an @Input() property in the child component class, receives its value from the parent's property, currentItem. When you click delete, the child component raises an event, deleteRequest, which is the argument for the parent's crossOffItem() method.

The following diagram shows the different parts of the @Input() and @Output() on the <app-input-output> child component.
  
 ![image of Input](https://angular.io/generated/images/guide/inputs-outputs/input-output-diagram.svg)
 


reference [https://stackblitz.com/edit/thvangular8-input]
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

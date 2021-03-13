reference [https://stackblitz.com/edit/thvangular8-input]
## @Input() and @Output() properties

- @Input() and @Output() allow Angular to share data between the parent context and child directives or components. An @Input() property is writable while an @Output() property is observable

### Sending data to a child component
- The ```@Input()``` decorator in a child component or directive signifies that the property can receive its value from its parent component.

![image of Input](https://angular.io/generated/images/guide/inputs-outputs/input.svg)

<b>To use @Input(), you must configure the parent and child.</b>

### Configuring the child component

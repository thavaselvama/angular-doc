# [Forms](https://angular.io/guide/forms-overview)
 - Angular provides two different approaches to handling user input through forms: 
 - <b>reactive</b> and <b>template-driven</b>.
 - Both capture user input events from the view, validate the user input, create a form model and data model to update, and      provide a way to track changes.

## [Reactive forms](https://angular.io/guide/reactive-forms) : 

 - Reactive forms are more robust: they're more scalable, reusable, and testable.
 - If forms are a key part of your application, or you're already using reactive patterns for building your application, use reactive forms.
## [Template-driven](https://angular.io/guide/forms) 
 - Template-driven forms are useful for adding a simple form to an app, such as an email list signup form. 
 - They're easy to add to an app, but they don't scale as well as reactive forms. 
 - If you have very basic form requirements and logic that can be managed solely in the template, use template-driven forms.
 
 ### Key differences
 
 common key | REACTIVE | TEMPLATE-DRIVEN
------------ | ------------- | -------------
Setup (form model)	 | More explicit, created in component class	 | Less explicit, created by directives
Data model	| Structured	| Unstructured
Predictability |	Synchronous |	Asynchronous
Form validation |	Functions | Directives
Mutability |	Immutable |	Mutable
Scalability |	Low-level API access |	Abstraction on top of APIs.

### Common foundation
- [FormControl](https://angular.io/api/forms/FormControl) tracks the value and validation status of an individual form control.

- [FormGroup](https://angular.io/api/forms/FormGroup) tracks the same values and status for a collection of form controls.

- [FormArray](https://angular.io/api/forms/FormArray) tracks the same values and status for an array of form controls.

- [ControlValueAccessor](https://angular.io/api/forms/ControlValueAccessor) creates a bridge between Angular FormControl instances and native DOM elements.
 
 ### Form model setup 
   #### Setup in reactive forms
   ```
   import { Component } from '@angular/core';
import { FormControl } from '@angular/forms';

@Component({
  selector: 'app-reactive-favorite-color',
  template: `
    Favorite Color: <input type="text" [formControl]="favoriteColorControl">
  `
})
export class FavoriteColorComponent {
  favoriteColorControl = new FormControl('');
}
```
![key](https://github.com/thavaselvama/angular-doc/blob/master/img/key-diff-reactive-forms.png)
  #### Setup in template-driven forms
  ```
  import { Component } from '@angular/core';

@Component({
  selector: 'app-template-favorite-color',
  template: `
    Favorite Color: <input type="text" [(ngModel)]="favoriteColor">
  `
})
export class FavoriteColorComponent {
  favoriteColor = '';
}
```
![](https://github.com/thavaselvama/angular-doc/blob/master/img/key-diff-td-forms.png)

#### Data flow in reactive forms
![](https://github.com/thavaselvama/angular-doc/blob/master/img/dataflow-reactive-forms-vtm.png)

 - The steps below outline the data flow from view to model.

     - The user types a value into the input element, in this case the favorite color Blue.
     - The form input element emits an "input" event with the latest value.
     - The control value accessor listening for events on the form input element immediately relays the new value to the FormControl instance.
     - The FormControl instance emits the new value through the valueChanges observable.
     Any subscribers to the valueChanges observable receive the new value.
     
!()(https://github.com/thavaselvama/angular-doc/blob/master/img/dataflow-reactive-forms-mtv.png).
 
 - The steps below outline the data flow from model to view.

    - The user calls the favoriteColorControl.setValue() method, which updates the FormControl value.
    - The FormControl instance emits the new value through the valueChanges observable.
    - Any subscribers to the valueChanges observable receive the new value.
    - The control value accessor on the form input element updates the element with the new value.
#### Data flow in template-driven forms:
 - In template-driven forms, each form element is linked to a directive that manages the form model internally. 
 - The diagrams below use the same favorite color example to demonstrate how data flows when an input field's value is changed from the view and then from the model.

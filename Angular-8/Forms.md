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
 

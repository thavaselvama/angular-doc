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


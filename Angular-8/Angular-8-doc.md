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

<img [src]="itemImageUrl2">


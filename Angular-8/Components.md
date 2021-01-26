# [Angular Components](https://angular.io/guide/component-overview#angular-components-overview )




 Components are the main building block for Angular applications. Each component consists of:
 
  * An HTML template that declares what renders on the page
  ```
 A template file, <component-name>.component.html
 
 ```
  * A Typescript class that defines behavior
  ```
  A component file, <component-name>.component.ts
  ```
  * A CSS selector that defines how the component is used in a template
  ```
  A CSS file, <component-name>.component.css
  ```
  * Optionally, CSS styles applied to the template
  ```
  styleUrls: ['./component-overview.component.css']
  ```
  ## Creating a component using the Angular CLI
  - Run the ng generate component <component-name> 
  example : ng g c example-component --spec false  /// if you don't want spec file
  
  * Creating a component
   - let we create component-overview
   ```
   import { Component } from '@angular/core';
   ```
```
@Component({ -- @Component decorator
  selector: 'app-component-overview', --> CSS selector for the component.
  templateUrl: './component-overview.component.html',
})
```
# Specifying a component's CSS selector
- Every component requires a CSS selector. 
- A selector instructs Angular to instantiate this component wherever it finds the corresponding tag in template HTML.
- For example, consider a component hello-world.component.ts that defines its selector as app-hello-world. This selector instructs Angular to instantiate this component any time the tag <app-hello-world> appears in a template.

Specify a component's selector by adding a selector statement to the @Component decorator.
```
@Component({
  selector: 'app-component-overview',
})
```

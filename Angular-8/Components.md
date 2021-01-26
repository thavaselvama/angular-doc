# Angular Components
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
  example : ng g c example-component --spec false /// if you don't want spec file

# NgModules
[Default doc link](https://angular.io/guide/ngmodules)
- <b>NgModules</b> configure the injector and the compiler and help organize related things together.
- An NgModule is a class marked by the @NgModule decorator. 
-  @NgModule takes a metadata object that describes how to compile a component's template and how to create an injector at runtime.
- It identifies the module's own components, directives, and pipes, making some of them public, through the exports property, so that external components can use them.
- @NgModule can also add service providers to the application dependency injectors.

```
// imports
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';

// @NgModule decorator with its metadata
@NgModule({
  declarations: [AppComponent], //The components, directives, and pipes that belong to this NgModule.
  
  imports: [BrowserModule], // The subset of declarations that should be visible and usable 
                                 in the component templates of other NgModules.
  providers: [],   // Creators of services that this NgModule contributes to the global collection of services; 
                     they become accessible in all parts of the app. 
                     (You can also specify providers at the component level, which is often preferred.)
                     
  bootstrap: [AppComponent] // The main application view, called the root component, which hosts all other app views. 
                               Only the root NgModule should set the bootstrap property.
})
export class AppModule {}
```
![Angular](https://github.com/thavaselvama/angular-doc/blob/master/img/angular-architecture.png)

## JavaScript modules vs. NgModules
### JavaScript modules
 - In JavaScript, modules are individual files with JavaScript code in them.
 ```
 import { AppComponent } from './app.component';
 ```
 - [JavaScript modules](https://hacks.mozilla.org/2015/08/es6-in-depth-modules/) help you namespace, preventing accidental global variables.
 
## NgModules

- NgModules are classes decorated with @NgModule. 
- The @NgModule decorator’s imports array tells Angular what other NgModules the current module needs.
```
/* These are JavaScript import statements. Angular doesn’t know anything about these. */
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';

/* The @NgModule decorator lets Angular know that this is an NgModule. */
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [     /* These are NgModule imports. */
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```
NgModule | JavaScript module
------------ | -------------
An NgModule bounds declarable classes only. Declarables are the only classes that matter to the Angular compiler. | Instead of defining all member classes in one giant file as in a JavaScript module, you list the module's classes in the @NgModule.declarations list.
An NgModule can only export the declarable classes it owns or imports from other modules. It doesn't declare or export any other kind of class. | Unlike JavaScript modules, an NgModule can extend the entire application with services by adding providers to the @NgModule.providers list.

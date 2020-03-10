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

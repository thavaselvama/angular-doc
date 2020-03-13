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

## Common module

NgModule | Import it from	 | Why you use it
------------ | ------------- | -------------
BrowserModule | @angular/platform-browser | When you want to run your app in a browser
CommonModule | 	@angular/common | When you want to use NgIf, NgFor
FormsModule | @angular/forms | When you want to build template driven forms (includes NgModel)
ReactiveFormsModule | @angular/forms | When you want to build reactive forms
RouterModule | @angular/router | When you want to use RouterLink, .forRoot(), and .forChild()
HttpClientModule |@angular/common/http | When you want to talk to a server
Observable | rxjs/Observable | Emit data Observable using
Observer | rxjs/Observer | Observer
Subject | rxjs/Subject | Observable and subscribe you can do at the time
ActivatedRoute | @angular/router | it carries the information about a route linked
Params | @angular/router | Observable of the matrix 

## Types of feature modules
1.Domain feature modules.

2.Routed feature modules.

3.Routing modules.

4.Service feature modules.

5.Widget feature modules.

<table>
 <tbody><tr>
   <th style="vertical-align: top">
     Feature Module
   </th>
   <th style="vertical-align: top">
     Guidelines
   </th>
 </tr>
 <tr>
   <td>Domain</td>
   <td>
     Domain feature modules deliver a user experience dedicated to a particular application domain like editing a customer or placing an order.
<p>     They typically have a top component that acts as the feature root and private, supporting sub-components descend from it.</p>
<p>     Domain feature modules consist mostly of declarations. Only the top component is exported.</p>
<p>     Domain feature modules rarely have providers. When they do, the lifetime of the provided services should be the same as the lifetime of the module.</p>
<p>     Domain feature modules are typically imported exactly once by a larger feature module.</p>
<p>     They might be imported by the root <code>AppModule</code> of a small application that lacks routing.</p>
   </td>
 </tr>
 <tr>
   <td>Routed</td>
   <td>
     Routed feature modules are domain feature modules whose top components are the targets of router navigation routes.
<p>     All lazy-loaded modules are routed feature modules by definition.</p>
<p>     Routed feature modules don’t export anything because their components never appear in the template of an external component.</p>
<p>     A lazy-loaded routed feature module should not be imported by any module. Doing so would trigger an eager load, defeating the purpose of lazy loading.That means you won’t see them mentioned among the <code>AppModule</code> imports. An eager loaded routed feature module must be imported by another module so that the compiler learns about its components.</p>
<p>     Routed feature modules rarely have providers for reasons explained in <a href="/guide/lazy-loading-ngmodules">Lazy Loading Feature Modules</a>. When they do, the lifetime of the provided services should be the same as the lifetime of the module. Don't provide application-wide singleton services in a routed feature module or in a module that the routed module imports.</p>
   </td>
 </tr>
 <tr>
   <td>Routing</td>
   <td>
<p>     A routing module provides routing configuration for another module and separates routing concerns from its companion module.</p>
<p>     A routing module typically does the following:</p>
     <ul>
     <li>Defines routes.</li>
     <li>Adds router configuration to the module's imports.</li>
     <li>Adds guard and resolver service providers to the module's providers.</li>
     <li>The name of the routing module should parallel the name of its companion module, using the suffix "Routing". For example, <code>FooModule</code> in <code>foo.module.ts</code> has a routing module named <code>FooRoutingModule</code> in <code>foo-routing.module.ts</code>. If the companion module is the root <code>AppModule</code>, the <code>AppRoutingModule</code> adds router configuration to its imports with <code>RouterModule.forRoot(routes)</code>. All other routing modules are children that import <code>RouterModule.forChild(routes)</code>.</li>
     <li>A routing module re-exports the <code><a href="api/router/RouterModule" class="code-anchor">RouterModule</a></code> as a convenience so that components of the companion module have access to router directives such as <code><a href="api/router/RouterLink" class="code-anchor">RouterLink</a></code> and <code><a href="api/router/RouterOutlet" class="code-anchor">RouterOutlet</a></code>.</li>
     <li>A routing module does not have its own declarations. Components, directives, and pipes are the responsibility of the feature module, not the routing module.</li>
     </ul>
<p>     A routing module should only be imported by its companion module.</p>
   </td>
 </tr>
 <tr>
   <td>Service</td>
   <td>
<p>     Service modules provide utility services such as data access and messaging. Ideally, they consist entirely of providers and have no declarations. Angular's <code><a href="api/common/http/HttpClientModule" class="code-anchor">HttpClientModule</a></code> is a good example of a service module.</p>
<p>     The root <code>AppModule</code> is the only module that should import service modules.</p>
   </td>
 </tr>
 <tr>
   <td>Widget</td>
   <td>
<p>     A widget module makes components, directives, and pipes available to external modules. Many third-party UI component libraries are widget modules.</p>
<p>     A widget module should consist entirely of declarations, most of them exported.</p>
<p>     A widget module should rarely have providers.</p>
<p>     Import widget modules in any module whose component templates need the widgets.</p>
   </td>
 </tr>
</tbody>
</table>

- The following table summarizes the key characteristics of each feature module group

<table>
 <tbody><tr>
   <th style="vertical-align: top">
     Feature Module
   </th>
   <th style="vertical-align: top">
     Declarations
   </th>
   <th style="vertical-align: top">
     Providers
   </th>
   <th style="vertical-align: top">
     Exports
   </th>
   <th style="vertical-align: top">
     Imported by
   </th>
 </tr>
 <tr>
   <td>Domain</td>
   <td>Yes</td>
   <td>Rare</td>
   <td>Top component</td>
   <td>Feature, AppModule</td>
 </tr>
 <tr>
   <td>Routed</td>
   <td>Yes</td>
   <td>Rare</td>
   <td>No</td>
   <td>None</td>
 </tr>
 <tr>
   <td>Routing</td>
   <td>No</td>
   <td>Yes (Guards)</td>
   <td>RouterModule</td>
   <td>Feature (for routing)</td>
 </tr>
 <tr>
   <td>Service</td>
   <td>No</td>
   <td>Yes</td>
   <td>No</td>
   <td>AppModule</td>
 </tr>
 <tr>
   <td>Widget</td>
   <td>Yes</td>
   <td>Rare</td>
   <td>Yes</td>
   <td>Feature</td>
 </tr>
</tbody></table>

## Entry components
- An entry component is any component that Angular loads imperatively, (which means you’re not referencing it in the template), by type. You specify an entry component by bootstrapping it in an NgModule, or including it in a routing definition.

- There are two main kinds of entry components:

   - The bootstrapped root component.
   - A component you specify in a route definition.
### A bootstrapped entry component
 - A bootstrapped component is an entry component that Angular loads into the DOM during the bootstrap process (application launch). Other entry components are loaded dynamically by other means, such as with the router.

- Angular loads a root AppComponent dynamically because it's listed by type in @NgModule.bootstrap.

```
@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    FormsModule,
    HttpClientModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent] // bootstrapped entry component
})
```
### A routed entry component
 - All router components must be entry components. Because this would require you to add the component in two places (router and entryComponents) the Compiler is smart enough to recognize that this is a router definition and automatically add the router component into entryComponents.

```
const routes: Routes = [
  {
    path: '',
    component: CustomerListComponent
  }
];
```
## [Feature modules](https://stackblitz.com/angular/rxnnrbrrllk?file=src%2Fapp%2Fcustomer-dashboard%2Fcustomer-dashboard.module.ts)

 - A feature module collaborates with the root module and with other modules through the services it provides and the components, directives, and pipes that it shares
 - create seprate module with in component and to use in rootmodule.
## [Providers](https://run.stackblitz.com/api/angular/v1?file=src/app/app.component.ts)
- A provider is an instruction to the Dependency Injection system on how to obtain a value for a dependency. 
### providedIn and NgModules 
 - It's also possible to specify that a service should be provided in a particular @NgModule.
 
 ```
 import { Injectable } from '@angular/core';
import { UserModule } from './user.module';

@Injectable({
  providedIn: UserModule,
})
export class UserService {
}
```
```
import { NgModule } from '@angular/core';

import { UserService } from './user.service';

@NgModule({
  providers: [UserService],
})
export class UserModule {
}
```
## [Singleton services](https://angular.io/guide/singleton-services#singleton-services)
[example](https://stackblitz.com/angular/omylrbvppab?file=src%2Fapp%2Fapp.module.ts)

- A singleton service is a service for which only one instance exists in an app.
   - That mean one service use many component using ```@Injectable() to "root"``` 
   - Add route module provide : [sampleService]. this instance use across the application sigle instance.
   
Example : 

- create service UserService you can use across the application if registor ```@NgModule({..  providers: [UserService],...})```
- Incause you registor one component(hero) you can't use other component(herodetails).

## [Lazy-loading feature modules](https://angular.io/guide/lazy-loading-ngmodules#lazy-loading-feature-modules)
[example](https://stackblitz.com/angular/pdbkggrbejy?file=src%2Fapp%2Fapp.module.ts)

- NgModules will load all which is module <b>declarations and imports</b>. whether its immediately necessary or not.
-  For large apps with lots of routes, consider lazy loading—a design pattern that loads NgModules as needed.
-  Lazy loading helps keep initial bundle sizes smaller, which in turn helps decrease load times.

## [Sharing modules](https://angular.io/guide/sharing-ngmodules)
- Creating shared modules allows you to organize and streamline your code. 
- You can put commonly used directives, pipes, and components into one module and then import just that module wherever you need it in other parts of your app.

[example](https://stackblitz.com/edit/angular8materials) : 
- here materials is shared module, which module you want just include ``` imports: [DemoMaterialModule]```
   - It imports the CommonModule because the module's component needs common directives.
   - It declares and exports the utility pipe, directive, and component classes.
   - It re-exports the CommonModule and FormsModule.
   

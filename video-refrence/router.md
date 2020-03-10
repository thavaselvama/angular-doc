## Router

### Routing and navigation
 - The Angular Router enables navigation from one view to the next as users perform application tasks.
 
[default example ](https://angular.io/generated/live-examples/router/stackblitz)

- basic packege import

```
import { ActivatedRoute, Params } from '@angular/router';
```
## ActivatedRoute
- Angular offers ActivatedRoute interface class, it carries the information about a route linked to a component loaded into the Angular app template. An ActivatedRoute contains the router state tree within the angular app’s memory.

## Understand ActivatedRoute Interface Class Properties

- Snapshot – This is the current snapshot of this route.
- URL – It is an observable of the URL segments and it matched by this route
- Params – Observable of the matrix parameters scoped to this route
- QueryParams – Observable of the query parameters shared by all the routes
- Fragment – Observable of the URL fragment shared by all the routes
- Data – Observable of the static and resolved data of this route.
- Root – This is the root of the router state
- Parent – This property is the parent of this route in the router state tree
- FirstChild – First child of this route in the router state tree
- Children – Children of this route in the router state tree
- pathFromRoot – Path from the root of the router state tree to this route
- paramMap – It is read-only
- queryParamMap – It is read-only
- Outlet – It’s a constant and outlet name of the route
- Component – It’s a constant and a component of the route
- RouteConfig – This configuration used to match this route

## dynamic route
 ```
 { path: 'product:id', component : productComponent},
 ```
 This colon tell this dynamic,in will take with in 
 
 - retrive route parameter following example
 
 ```
 import { Component, OnInit } from '@angular/core';
import { ActivatedRoute,Params } from '@angular/router'

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit {
  user: {id: number, name: string};

  constructor( private avtivateRoute : ActivatedRoute) { }

  ngOnInit() {
    this.user = {
      id : this.avtivateRoute.snapshot.params['id'],
      name : this.avtivateRoute.snapshot.params['name']
    }
    console.log(this.user)
  }

}
 ```
 
 ```
 User {{user.id}} is  {{user.name}}
 ```
 
  - If programaticatally load url params its don't chage in html
  
example 

[routerLink]="['/user',10,'test']"


- When you use brackets, it means you're passing a bindable property (a variable).

  ```
  User {{user.id}} is  {{user.name}}
  ```
  
  because same component cant reload 
  
  ```
  
  ngOnInit() {
    this.user = {
      id : this.activateRoute.snapshot.params['id'],
      name : this.activateRoute.snapshot.params['name']
    };
    this.route.params
    .subscribe(
    (params : Params) =>{
    this.user.id = params['id'],
    this.user.name = params['name'],
    }
    )
  }

  ```
  note : 
 - when you leave that particular component angular destroy component behind the screen. but subscribe its keep in the menory
 - if u wants destory subscribe you can add destroy lifecycle hook
 
 ```
import { Component, OnInit,OnDestroy } from '@angular/core';
import { ActivatedRoute,Params } from '@angular/router'
import { Subscription } from 'rxjs/Subscription';


@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit,OnDestroy {
  user: {id: number, name: string};
  paramSubcribition : Subscription;
   constructor( private avtivateRoute : ActivatedRoute) { }

  ngOnInit() {
    this.user = {
      id : this.avtivateRoute.snapshot.params['id'],
      name : this.avtivateRoute.snapshot.params['name']
    };
    this.paramSubcribition = this.route.params
    .subscribe(
    (params : Params) =>{
    this.user.id = params['id'],
    this.user.name = params['name'],
    }
    )
    
  }
  ngOnDestroy(){
   this.paramSubcribition.unSubscribe();
  }

}
 ```
## RXJS
 - rxjs offering all observing functionality. Angular use this packege.
 - Subscription use to destory memory
 
 ## Query params
 
 ```
 this.router.navigate(['/servers',5,'edit'], [queryParams] = {'allowedit : 1'});
 ```
 
 its will display in URL 
 
 ```
 servers/5/edit?allowedit=1
 ```
 
 ## Child Routes

```
const routes: Routes = [
  {
    path: '',
    component: RecipesComponent,
  },
  {
    path: 'recipe',
    component: RecipesComponent,
    children: [
      { path: '', component: RecipeStartComponent },
    ]
  },
  {
    path: 'shopping-list',
    component: ShoppingListComponent,
  },
];
```
- inject <router-outlet></router-outlet> in your parent component

```
<div class="row">
  <div class="col-md-5">
<app-recipe-list ></app-recipe-list>
  </div>
  <div class="col-md-7">
<router-outlet></router-outlet>

  </div>
</div>
```
 

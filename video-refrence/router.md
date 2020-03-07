## Router

### Routing and navigation
 - The Angular Router enables navigation from one view to the next as users perform application tasks.
 
[default example ](https://angular.io/generated/live-examples/router/stackblitz)


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

[routerLink="['/user',10,'test']"
  
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



 
 

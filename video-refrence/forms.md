# Forms
[Angular form](https://angular.io/guide/forms-overview)

[Custom](https://stackblitz.com/edit/angular-form-video?file=src%2Fapp%2Fapp.component.html)

- Handling user input with forms is the cornerstone of many common applications.
There are two type of forms.

1.Reactive forms - are more robust: they're more scalable, reusable, and testable. If forms are a key part of your application, or you're already using reactive patterns for building your application, use reactive forms.


2.Template-driven forms :  are useful for adding a simple form to an app, such as an email list signup form. They're easy to add to an app, but they don't scale as well as reactive forms. If you have very basic form requirements and logic that can be managed solely in the template, use template-driven forms.

- Receive form from html to controller using ngForm ```<form (ngSubmit)="onSubmit()" #heroForm="ngForm">```

``` 
import { NgForm } from '@angular/forms';
onSubmit( form : NgForm){
 console.log(form)
 }
 ``` 
 Another Example : 
 ```
 import { Component,ViewChild } from '@angular/core';
 @ViewChild('f') sineUpForm : NgForm;
  onSubmit( ){
  console.log(this.sineUpForm)
  }
 ```
 
 - Both output same as the following 
 
 ![](https://github.com/thavaselvama/angular-doc/blob/master/img/form-sample.png.png)
 
 ## Form validations  ```<form (ngSubmit)="onSubmit()" #f="ngForm" >```
 ```
 <button [disabled]="!f.valid" class="btn btn-primary" type="submit">Submit</button>
 ```
  - individual field validate set 
  ```<input type="email" id="email" name="email" class="form-control" 
         ngModel required email #email="ngModel">
      <div *ngIf="!email.valid && email.touched "> Please enter valid email id</div>
 ```
 

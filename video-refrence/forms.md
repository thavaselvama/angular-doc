# Forms
[Angular form](https://angular.io/guide/forms-overview)

[Custom](https://stackblitz.com/edit/angular-form-video?file=src%2Fapp%2Fapp.component.html)

- Handling user input with forms is the cornerstone of many common applications.
There are two type of forms.

1.Reactive forms - are more robust: they're more scalable, reusable, and testable. If forms are a key part of your application, or you're already using reactive patterns for building your application, use reactive forms.


2.Template-driven forms :  are useful for adding a simple form to an app, such as an email list signup form. They're easy to add to an app, but they don't scale as well as reactive forms. If you have very basic form requirements and logic that can be managed solely in the template, use template-driven forms.
## Template-driven forms
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
 - #email="ngModel" Angular NgModel directive associated with this control that you can use in the template to check for control states such as valid and dirty
 
 - you can combine list of fileds in a group using <b><div id="user-data" ngModelGroup="userData" #userData="ngModelGroup"></b>.
 - and you create group of object. what is added fields in that group.
 - you can validate list of groups.
 
 example :
 
 ```
 <h3>Form</h3>
<h5>Template-driven forms</h5>

<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-10 col-md-8 col-sm-offset-1 col-md-offset-2">
      <form (ngSubmit)="onSubmit()" #f="ngForm" >
        <div id="user-data" ngModelGroup="userData" #userData="ngModelGroup">
          <div class="form-group">
            <label for="username">Username</label>
            <input type="text" id="username" name="username" class="form-control" ngModel required>
          </div>
          <button class="btn btn-default" type="button">Suggest an Username</button>
          <div class="form-group">
            <label for="email">Mail</label>
            <input type="email" id="email" name="email" class="form-control" 
            ngModel required email #email="ngModel">
          </div>
          <div *ngIf="!email.valid && email.touched "> Please enter valid email id</div>
        </div>
        <div  *ngIf="!userData.valid && userData.touched ">
          Please enter
        </div>
        <div class="form-group">
          <label for="secret">Secret Questions</label>
          <select id="secret" name="secret" [ngModel]="defaultSelect" class="form-control" required>
            <option value="pet">Your first Pet?</option>
            <option value="teacher">Your first teacher?</option>
          </select>
        </div>
        <div class="form-group">
          <textarea name="question" class="form-control" [(ngModel)]="question"></textarea>
        </div>
        <p>You reply as {{question}}</p>
        <button [disabled]="!f.valid" class="btn btn-primary" type="submit">Submit</button>

      </form>
    </div>
  </div>
</div>

```
- set all value control in one command - It will set all those value inside form

```
 <button class="btn btn-default"
           type="button" (click)="setSuperUser()">
           Suggest an Username</button>
  ```
  - but this not best approch - it will set particular value - no need to enter other value like (email,secret)
  ```
  setSuperUser(){
    this.sineUpForm.form.setValue({
      userData :{
        username : "suggestedName",
        email : ''
      },
      secret : 'pet',
      question : '',
      gender : 'Female'

    })
  }
  ```
  - best Approch 
  ```
  this.sineUpForm.form.patchValue({
      userData :{
        username : "suggestedName", 
      }
    })
  ```
 ## reactive-form
 
 - import  ```import { ReactiveFormsModule } from '@angular/forms';``` in module
 - import FormGroup ```import { FormGroup,FormControl,Validators } from '@angular/forms';```
 ```
  <form [formGroup]="signupForm" (ngSubmit)="onSubmit()">
 <div formGroupName="userData">
			<div class="form-group">
				<label for="username">Username</label>
				<input
		            type="text"
		            id="username"
		            formControlName="username"
		            class="form-control">
		        </div>
				<span *ngIf="!signupForm.get('userData.username').valid && signupForm.get('userData.username').touched"> Please enter valid name</span>
				<div class="form-group">
					<label for="email">email</label>
					<input
		            type="text"
		            id="email"
		             formControlName="email"
		            class="form-control">
		        </div>
					<span *ngIf="!signupForm.get('userData.email').valid && signupForm.get('userData.email').touched"> Please enter valid email</span>
				</div>
    
  ```
  
  ```
  signupForm : FormGroup;
   ngOnInit() {
    this.signupForm = new FormGroup({
      'userData' :new FormGroup({
 'username' : new FormControl(null,Validators.required),
      'email' : new FormControl(null,[Validators.required,Validators.email]),
      
    }),
    'gender' : new FormControl('male',Validators.required)
      }) 
  }
  ```
  
  
  
 
  
  
 

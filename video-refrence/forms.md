# Forms
[Angular form](https://angular.io/guide/forms-overview)

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
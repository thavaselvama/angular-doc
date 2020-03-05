
# Component interaction
 - This cookbook contains recipes for common component communication scenarios in which two or more components share information.
 
 [link to default](https://stackblitz.com/angular/jdevvqplyjr?file=src%2Fapp%2Fapp.component.html)
 
 [link to Custom](https://stackblitz.com/edit/component-interaction-thavaselvam?file=src%2Fapp%2Fapp.component.html)
 
## Pass data from parent to child with input binding
```
import { Component,OnInt } from '@angular/core';
import { products } from './products';
@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.css' ]
})
export class AppComponent implements OnInit  {
  name = 'Angular';
products = products;

ngOnInit() {

}
}
```
```
<app-product-details [productDetails]= 'products'></app-product-details>
```
```
import { Component, OnInit,Input } from '@angular/core';

@Component({
  selector: 'app-product-details',
  templateUrl: './product-details.component.html',
  styleUrls: ['./product-details.component.css']
})
export class ProductDetailsComponent implements OnInit {
@Input() productDetails;
  constructor() { }

  ngOnInit() {
    console.log(this.productDetails)
  }

}
```
@Input receive data from parents to child.

## Parent listens for child event

Passing data from child to parent using @Output

```
import { Component, OnInit,Output,EventEmitter } from '@angular/core';
import { products } from '../products';
@Component({
  selector: 'app-product-click',
  templateUrl: './product-click.component.html',
  styleUrls: ['./product-click.component.css']
})
export class ProductClickComponent implements OnInit {
products = products;
@Output() productSlct = new EventEmitter<any>();
  constructor() { }

  ngOnInit() {
  }
selectProduct(select){
this.productSlct.emit(select)
}
}
```
````
<h4>Parent listens for child event</h4>
<app-product-click (productSlct)="selectedProductDetails($event)"></app-product-click>
````
```
selectedProductDetails(data){
  console.log(data)
this.selectedData = data;
}
```

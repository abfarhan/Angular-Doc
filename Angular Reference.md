
## **Each next subscribers receive**

> Subject :- only upcoming values
>
> BehaviorSubject :- one previous value and upcoming values
>
> ReplaySubject :- all previous values and upcoming values
>
> AsyncSubject :- the latest value when the stream will close

Refer for [more](http://reactivex.io/documentation/subject.html)

## **cloneDeep**

> npm i lodash

``` typescript
import { cloneDeep } from 'lodash';
```

## **observableOf**

``` typescript
import { of as observableOf } from 'rxjs';

export class MockStickyNotesFacade {
    public loadNotes() {
     return observableOf(cloneDeep(MockPatientNotes));
    }
}
```

## **unsubscribing**
  
``` typescript
private unsubscribe: Subject<void> = new Subject();

 this.someMethod
    .pipe(takeUntil(this.unsubscribe))
    .subscribe(
      // some operation
	);

 ngOnDestroy() {
    this.unsubscribe.next();
    this.unsubscribe.complete();
  }
```
  
  
## **Proxying to a backend server**

### To connect the frontend to backend we need to use proxyConfig

 1. Create a file proxy.conf.json in your project.
 2. Add the following content to the new proxy file:

``` json
	{
		"/ECommerse": {
			"target": "http://localhost:1405",
			"secure": false
		}
	}
```

> In the service the code looks like below,

``` typescript
	 public getAllProducts() {
        return this.http.get<any[]>(`/ECommerse/products`);
    }
```

 3. There are 2 ways to do the 3rd step,

	1. In angular.json, add the proxyConfig option to the serve target:

	``` json
		"architect": {
		  "serve": {
			"builder": "@angular-devkit/build-angular:dev-server",
			"options": {
			  "browserTarget": "your-application-name:build",
			  "proxyConfig": "proxy.conf.json"
			},
		```

 	2. In package.json add proxy config to the start script.

		``` json
		"scripts": {
			"ng": "ng",
			"start": "ng serve -o --proxy-config proxy.conf.json",
		},
		```

For more click [here](https://angular.io/guide/build#proxying-to-a-backend-server)


## **Component interaction (communication) using service**

### **Method 1 :-**

> create a service :- 

``` typescript
	import { Injectable } from '@angular/core';
	import { BehaviorSubject } from 'rxjs';

	@Injectable()
	export class ProductHelperService {
		public currentPage = new BehaviorSubject<string>('Product List');
	}
```

> In one component set the current page value

``` typescript
    this.productHelperService.currentPage.next('Add Product');
``` 
 
> In other component subscribe to the value 

``` typescript
	 this.subscription = this.productHelperService.currentPage.subscribe((val) => {
      this.currentPage = val;
    });
```


### **Method 2 :-**

> create a service :- 

``` typescript
	import { Injectable } from '@angular/core';
	import { BehaviorSubject } from 'rxjs';

	@Injectable()
	export class ProductHelperService {

	private currentPageSource = new BehaviorSubject<string>('Product List');
	
	currentPage = this.currentPageSource.asObservable();
	
	setCurrentPage(currPage: string) {
  		this.currentPageSource.next(currPage);
		}
	}
```

> In one component set the current page value

``` typescript
 this.productHelperService.setCurrentPage('Add Product');
```

> In other component subscribe to the value 

``` typescript
	this.subscription = this.productHelperService.currentPage.subscribe((val) => {
		this.currentPage = val;
	});
```

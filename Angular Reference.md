
## **Each next subscribers receive**

> Subject :- only upcoming values
>
> BehaviorSubject :- one previous value and upcoming values
>
> ReplaySubject :- all previous values and upcoming values
>
> AsyncSubject :- the latest value when the stream will close

## Subject

```typescript
import { Component } from '@angular/core';
import { Subject } from 'rxjs';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent {
  mySunject$ = new Subject();

  ngOnInit() {
    this.mySunject$.next(1);

    this.mySunject$.subscribe((val) => console.log(val));

    this.mySunject$.next(2);
    this.mySunject$.next(3);
  }
}

Output:
2
3
```
Subject only get notified of the events after we subscribe to it. 
Here the value `1` is send before we subscribe to `mySunject$`, so it is not logged in console.

```typescript
import { Component } from '@angular/core';

import { Subject } from 'rxjs';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent {
  mySunject$ = new Subject();

  ngOnInit() {
    this.mySunject$.subscribe((val) => console.log('first subscribe ' + val));

    this.mySunject$.next(1);
    this.mySunject$.next(2);
    this.mySunject$.next(3);

    this.mySunject$.subscribe((val) => console.log('second subscribe ' + val));
    this.mySunject$.next(4);
  }
}

Output:
first subscribe 1
first subscribe 2
first subscribe 3
first subscribe 4
second subscribe 4
```

## BehaviorSubject

A behavior subject is just like a subject except it requires a starting value and holds the most recent value for any new subscribers.

```typescript
import { Component } from '@angular/core';

import { BehaviorSubject } from 'rxjs';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent {
  mySunject$ = new BehaviorSubject(200);

  ngOnInit() {
    this.mySunject$.subscribe((val) => console.log('first subscribe ' + val));

    this.mySunject$.next(1);
    this.mySunject$.next(2);
    this.mySunject$.next(3);

    this.mySunject$.subscribe((val) => console.log('second subscribe ' + val));
    
    this.mySunject$.next(4);
  }
}

Output:
first subscribe 200
first subscribe 1
first subscribe 2
first subscribe 3
second subscribe 3
first subscribe 4
second subscribe 4
```

## ReplaySubject

The replay subject will save all the values and give them to each subscriber even after the replay subject has been completed.

```typescript
import { Component } from '@angular/core';

import { ReplaySubject } from 'rxjs';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent {
  mySunject$ = new ReplaySubject();

  ngOnInit() {
    this.mySunject$.subscribe((val) => console.log('first subscribe ' + val));

    this.mySunject$.next(1);
    this.mySunject$.next(2);
    this.mySunject$.next(3);

    this.mySunject$.subscribe((val) => console.log('second subscribe ' + val));
    this.mySunject$.next(4);
  }
}

Output:
first subscribe 1
first subscribe 2
first subscribe 3
second subscribe 1
second subscribe 2
second subscribe 3
first subscribe 4
second subscribe 4
```

## AsyncSubject

The AsyncSubject is a variant where only the last value of the Observable execution is sent to its observers, and only when the execution completes.

```typescript
import { Component } from '@angular/core';

import { AsyncSubject } from 'rxjs';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent {
  mySunject$ = new AsyncSubject();

  ngOnInit() {
    this.mySunject$.subscribe((val) => console.log('first subscribe ' + val));

    this.mySunject$.next(1);
    this.mySunject$.next(2);
    this.mySunject$.next(3);

    this.mySunject$.subscribe((val) => console.log('second subscribe ' + val));
    this.mySunject$.next(4);
    this.mySunject$.complete();
  }
}

Output:
first subscribe 4
second subscribe 4
```

Refer for [more](https://rxjs.dev/guide/subject)

## **of**

of converts the values into observable value.

```typescript
import { of } from 'rxjs';

export class AppComponent {
  screamWarrior;

  ngOnInit() {
    this.screamWarrior = of('samurai', 'ninja', 'viking', 'soldiers');
    this.screamWarrior.subscribe((val) => console.log(val));
  }
}
```

## **from**

from converts the array of values into observable value.

```typescript
import { from } from 'rxjs';

export class AppComponent {
  screamWarrior;

  ngOnInit() {
    this.screamWarrior = from(['samurai', 'ninja', 'viking', 'soldiers']);
    this.screamWarrior.subscribe((val) => console.log(val));
  }
}
```

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

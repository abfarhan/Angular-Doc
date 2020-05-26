![Prototype chain](https://github.com/abfarhan/Angular-Doc/blob/master/assets/angular%20doc.png?raw=true)

---

<center>⚠️ Work In Progress ⚠️</center>

---

### **Topics**:<br>

- [What is Angular](#what-is-angular)
- [ng-content](#ng-content)
- [Data Binding](#data-binding)
- [String interpolation](#string-interpolation)
- [Property binding](#property-binding)
- [Event binding](#event-binding)
- [Angular Authentication and Authorization](#angular-authentication-and-Authorization)
- [Difference between Angular and AngularJS](#difference-between-Angular-and-AngularJS)
- [Dependency Injection](#dependency-injection)
- [How angular application starts](#how-angular-application-starts)
- [Service](#service)
- [AsyncPipe](#asyncPipe)
- [Directives overview](#directives-overview)
- [Angular Compilation](#angular-compilation)
- [Why do we need compilation process](#why-do-we-need-compilation-process)
- [Binding to custom properties in angular](#binding-to-custom-properties-in-angular)
- [Binding to custom event](#binding-to-custom-event)
- [View Encapsulation](#view-encapsulation)
- [Local Reference (Template reference)](<#local-Reference-(template-reference)>)
- [@ViewChild](#@viewChild)
- [@ContentChild](#@contentChild)
- [Lifecycle hooks](#lifecycle-hooks)
- [Navigating between different routes](#navigating-between-different-routes)
- [Building blocks of Angular](#building-blocks-of-Angular)
- [Lazy-loading feature modules](#lazy-loading-feature-modules)
- [ng-template](#ng-template)
- [Custom directive](#custom-directive)
- [@HostListener() Decorator](<#@hostListener()-decorator>)
- [@HostBinding() Decorator](<#@hostBinding()-decorator>)
- [Binding to directive property](#binding-to-directive-property)
- [Creating custom structural directive](#creating-custom-structural-directive)
- [Router Link](#router-link)
- [Fetching route parameters](#fetching-route-parameters)
- [Query Parameters and Fragments](#query-Parameters-and-fragments)
- [Nested Route (child routes)](<#nested-route-(child-routes)>)
- [Handling query parameters](#handling-query-parameters)
- [Redirecting Routes](#redirecting-routes)
- [canActivate & canActivateChild](#canActivate-&-canActivateChild)
- [CanDeactivate](#canDeactivate)
- [Synchronous](#synchronous)
- [Asynchronous](#asynchronous)
- [RXJS (Reactive Extensions for JavaScript)](<#rxjs-(reactive-extensions-for-javaScript)>)
- [Observables](#observables)
- [Promise](#promise)
- [Promise vs Observable](#promise-vs-observable)
- [Difference between find() and filter()](<#difference-between-find()-and-filter()>)

## **What is Angular**

Angular is a TypeScript based open source web application framework, developed and maintained by Google.<br/>
It offers an easy and powerful way of building single page web-based applications.<br/>

## **ng-content**

ng-content is used for content projection.<br/>
You use the `<ng-content></ng-content>` tag as a placeholder for that dynamic content,
then when the template is parsed Angular will replace that placeholder tag with your content.<br/>
ng-content is very useful when creating component libraries or reusable components.

## **Data Binding**

It is the communication b/w the typescript code of the component and the HTML template.

    	* Interpolation
    	* One way binding (property binding)
    	* Two way binding
    	* Event binding

## **String interpolation**

string interpolation is a one way data binding technique which is used to display out put fron typescript code to html template.<br/>
Basically we can show dynamic values in html.

## **Property binding**

Binding HTML property with typescript property or data.

```
<input type="text" class="form-control" [(ngModel)]="userName">
<button class="btn btn-primary" [disabled]="userName === ''">Enter name</button>
```

## **Event binding**

In angular event binding is used to handle the events raised from the DOM like button click, mouse move etc.<br/>
When the DOM event happens (eg. click, change, keyup), it calls the specified method in the component

`<button (click)="onButtonClick()"></button>`

## **Event Bubbling**

When Angular attaches event handlers to standard HTML element events,
the event propagation works in the same way as standard DOM event propagation works. This is also called event bubbling.<br/>

Event bubbling allows a single handler on a parent element to listen to events fired by any of its children.

```
<div id="parent" (click)="doWork($event)"> Try
<div id="child">me!</div>
</div>
```

Clicking on either of the div results in the invocation of the doWork function on the parent div.<br/>
Moreover, \$event.target contains the reference to the div that dispatched the event.<br/>
Custom events created on Angular components do not support event bubbling.<br/>

## **Angular Authentication and Authorization**

The user login credentials are passed to an authenticate API, which is present on the server. <br/>
Post server-side validation of the credentials, a JWT (JSON Web Token) is returned. <br/>
The JWT has information or attributes regarding the current user. The user is then identified with the given JWT. This is called authentication.<br/>

Post logging-in successfully, different users have a different level of access.<br/>
While some may access everything, access for others might be restricted to only some resources. The level of access is authorization.

## **Difference between Angular and AngularJS**

- Architecture - AngularJS supports the MVC design model. Angular relies on components and directives instead
- Dependency Injection (DI) - Angular supports a hierarchical Dependency Injection with unidirectional tree-based change detection. AngularJS doesn’t support DI
- Mobile Support - AngularJS doesn’t have mobile support while Angular does have
- Recommended Language - While JavaScript is the recommended language for AngularJS, TypeScript is the recommended language for Angular

## **Dependency Injection**

Dependency Injection (DI) is a core concept of Angular 2+ and allows a class receive dependencies from another class. <br/>
Most of the time in Angular, dependency injection is done by injecting a service class into a component or module class.

## **How angular application starts**

- Angular started with main.ts.<br/>
- Main.ts file is the first code that gets executed.<br/>
- The job of main.ts is to bootstrap the application. It loads everything and controls the startup of the application.<br/>
- Inside main.ts file angular passes AppModule to the bootstrapModule() method.<br/>
- In app.module.ts file angular gives AppComponent in the bootstrap array.<br/>
- Bootstrap array list all the components which should be known to angular at the point of the time it analysis index.html.<br/>
- And angular now analyze this app component, reading the set up we pass there and recognises SELECTOR app-root.<br/>
- Now, angular is enable to handle app-root in the index.html.<br/>

> main.ts -> app.module -> AppComponent

angular adds scripts to the html with that angular code is able to parse app-root

## **Service**

A service is typically a class with a well-defined purpose. A service is used when a common functionality needs to be provided to various modules. <br/>
Services allow for greater seperation of concerns for your application and better modularity by allowing you to extract common functionality out of components. <br/>
Angular also comes with its own dependency injection framework for resolving dependencies, so you can have your services depend on other services throughout your application.

```
import { Injectable } from '@angular/core';
 import { Http } from '@angular/http';

 @Injectable({ // The Injectable decorator is required for dependency injection to work
   // providedIn option registers the service with a specific NgModule
   providedIn: 'root',  // This declares the service with the root app (AppModule)
 })
 export class RepoService{
   constructor(private http: Http){
   }

   fetchAll(){
     return this.http.get('https://api.github.com/repositories');
   }
 }
```

## **AsyncPipe**

The async pipe subscribes to an Observable or Promise and returns the latest value it has emitted. <br/>
When a new value is emitted, the async pipe marks the component to be checked for changes. <br/>
When the component gets destroyed, the async pipe unsubscribes automatically to avoid potential memory leaks. <br/>

```
@Component({
 selector: 'async-observable-pipe',
 template: '<div><code>observable|async</code>: Time: {{ time | async }}</div>'
})
export class AsyncObservablePipeComponent {
 time = new Observable<string>((observer: Observer<string>) => {
   setInterval(() => observer.next(new Date().toString()), 1000);
 });
}
```

## **Directives overview**

Directives are something that extends the functionality of html. <br>
There are three kinds of directives in Angular:

- Components — directives with a template.
- Structural directives — change the DOM layout by adding and removing DOM elements.
- Attribute directives — change the appearance or behavior of an element, component, or another directive.

-- structural directives
Structural directives—change the DOM layout by adding and removing DOM elements.

### **\*ngFor**

A structural directive that renders a template for each item in a collection.

```
<li *ngFor="let item of items; index as i; trackBy: trackByFn">...</li>
```

### **\*ngIf**

A structural directive that conditionally includes a template based on the value of an expression coerced to Boolean

```
<div *ngIf="condition; else elseBlock">Content to render when condition is true.</div>
<ng-template #elseBlock>Content to render when condition is false.</ng-template>
```

### **\*ngSwitch**

A structural directive that adds or removes templates (displaying or hiding views) when the next match expression matches the switch expression.

```
<container-element [ngSwitch]="switch_expression">
  <!-- the same view can be shown in more than one case -->
  <some-element *ngSwitchCase="match_expression_1">...</some-element>
  <some-element *ngSwitchCase="match_expression_2">...</some-element>
  <some-other-element *ngSwitchCase="match_expression_3">...</some-other-element>
  <!--default case when there are no matches -->
  <some-element *ngSwitchDefault>...</some-element>
</container-element>
```

## **Angular Compilation**

Angular offers two ways to compile your application:<br/>

- Just-in-Time (JIT), which compiles your app in the browser at runtime.<br/>
- Ahead-of-Time (AOT), which compiles your app at build time.<br/>

### **_AOT Compilation_**

The Angular ahead-of-time (AOT) compiler converts your Angular HTML and TypeScript code into efficient JavaScript
code during the build phase before the browser downloads and runs that code. <br/>
Compiling your application during the build process provides a faster rendering in the browser.<br/>

For AOT compilation, include the --aot option with the ng build or ng serve command:<br/>

- ng build --aot
- ng serve --aot

## **Why do we need compilation process**

An Angular application consists mainly of components and their HTML templates.<br/>
Because the components and templates provided by Angular cannot be understood by the browser directly,
Angular applications require a compilation process before they can run in a browser.

## **Binding to custom properties in angular**

using @Input()
passing data from parent component to child component

`<div [highlightColor] = "'orange'" ></div>`<br/>
------- or ------- <br/>
`<div highlightColor = "orange" ></div>`<br/>

Both are same. If we are using [] the we need to put our string in ' ' (single quote) inside " " (double quote).
If we are not using [] the we can put our string directly inside " " (double quote) and no need of '' (single quote).

## **Binding to custom event**

using @Output() and EventEmitter
passing data from child component to parent component

## **View Encapsulation**

Angular uses View Encapsulation to make use of shadow dom technique to add unique attribute to its element.
So that the styles of this component only applied inside the component.
To put simply, ViewEncapsulation determines whether the styles defined in a particular component will affect the entire application or not.

Angular supports 3 types of ViewEncapsulation:

- Emulated
- None
- ShadowDom

The default ViewEncapsulation is Emulated. We can remove the encapsulation by setting ViewEncapsulation to none
If we set the ViewEncapsulation to none they don't receive there unique selector therefore the styles written in that component
will be considered as global styles.

```
@Component({
  selector: 'my-app',
  templateUrl: './my-app.component.html',
  styleUrls: ['./my-app.component.css'],
  encapsulation: ViewEncapsulation.None
})
```

## **Local Reference (Template reference)**

Using template reference we can get access to some elements in the template and then use it either directly in the template
or pass it to the typescript code.

```
<div>
<input type="text" #thisIsTheReference />
</div>
<div >
<button (click)="onClickButton(thisIsTheReference)">Add Gift</button>
</div>
```

## **@ViewChild**

With @ViewChild (add { static: true } as a second argument) needs to be applied if you plan on accessing the selected element inside of ngOnInit().
If you DON'T access the selected element in ngOnInit (but anywhere else in your component), set static: false instead!
If you're using Angular 9, you only need to add { static: true } (if needed) but not { static: false }.

Using viewchild we can get access to the html element.

## **@ContentChild**

Using content child we can get access to the elements in the parent component.

## **Lifecycle hooks**

constructor is called first. Then followed by hooks.

ngOnChanges() accepts a parameter eg: ngOnChanges(changes: SimpleChanges) {}

- ngOnChanges()
- ngOnInit()
- ngDoCheck()
- ngAfterContentInit()
- ngAfterContentChecked()
- ngAfterViewInit()
- ngAfterViewChecked()
- ngOnDestroy()

## **Navigating between different routes**

```
<a class="nav-link" (click)="goHome()">Home</a>
<a class="nav-link" (click)="goSearch()">Search</a>

import {Router} from "@angular/router";

constructor(private router: Router) {}
  goHome() {
    this.router.navigate(['']);
  }
  goSearch() {
    this.router.navigate(['search']);
  }
```

## **Building blocks of Angular**

- Components
- Directives
- Dependency Injection (DI)
- Modules
- Routing
- Services
- Data Binding

## **Lazy-loading feature modules**

> src/app/app.component.html

```
<button routerLink="/customers">Customers</button>
<button routerLink="/orders">Orders</button>
<button routerLink="">Home</button>
```

> src/app/app-routing.module.ts

```
const routes: Routes = [
  {
    path: 'customers',
    loadChildren: () => import('./customers/customers.module').then(m => m.CustomersModule)
  },
  {
    path: 'orders',
    loadChildren: () => import('./orders/orders.module').then(m => m.OrdersModule)
  },
  {
    path: '',
    redirectTo: '',
    pathMatch: 'full'
  }
];
```

The first two paths are the routes to the CustomersModule and the OrdersModule.
The final entry defines a default route. The empty path matches everything that doesn't match an earlier path.

**Inside the feature module**

> src/app/customers/customers.module.ts

```
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { CustomersRoutingModule } from './customers-routing.module';
import { CustomersComponent } from './customers.component';

@NgModule({
 imports: [
   CommonModule,
   CustomersRoutingModule
 ],
 declarations: [CustomersComponent]
})
export class CustomersModule { }
```

> src/app/customers/customers-routing.module.ts

```
import { NgModule } from '@angular/core';
import { Routes, RouterModule } from '@angular/router';
import { CustomersComponent } from './customers.component';

const routes: Routes = [
  {
    path: '',
    component: CustomersComponent
  }
];

@NgModule({
  imports: [RouterModule.forChild(routes)],
  exports: [RouterModule]
})
export class CustomersRoutingModule { }
```

> src/app/orders/orders-routing.module.ts

```
import { OrdersComponent } from './orders.component';

const routes: Routes = [
  {
    path: '',
    component: OrdersComponent
  }
];
```

For detailed documentation **_[check](https://angular.io/guide/lazy-loading-ngmodules)_**

## **ng-template**

ng-template is a virtual element and its contents are displayed only when needed (based on conditions).
ng-template should be used along with structural directives like [ngIf],[ngFor],[NgSwitch] or custom structural directives.

```
<div *ngIf="condition; else elseBlock">Content to render when condition is true.</div>
<ng-template #elseBlock>Content to render when condition is false.</ng-template>
```

ng-template never meant to be used like other HTML elements. It’s an internal implementation of Angular’s structural directives.
When you use a structural directive in Angular we will add a prefix asterisk(_) before the directive name.
This asterisk is short hand notation for ng-template.
Whenever Angular encounter with the asterisk(_) symbol, we are informing Angular saying that it is a structural directive
and Angular will convert directive attribute to ng-template element.
ng-template is not exactly a true web element. When we compile our code, we will not see a ng-template tag in HTML DOM.
Angular will evaluate the ng-template element to convert it into a comment section in HTML DOM.

```
<div *ngIf="display" class="ng-template-example">
 ng-template example
</div>

<!-- Converted Element -->
<ng-template [ngIf]="display">
 <div class="ng-template-example">ng-template example</div>
</ng-template>
```

The directive being converted to data member of ng-template
The inline template element along with the attributes (class etc), moved inside the ng-template element

For detailed documentation **[check](https://www.freecodecamp.org/news/everything-you-need-to-know-about-ng-template-ng-content-ng-container-and-ngtemplateoutlet-4b7b51223691/)**

## **Custom directive**

```
import { Directive, ElementRef, OnInit } from '@angular/core'

@Directive({
  selector: '[appExample]',
})
export class ExampleDirective implements OnInit {
  constructor(private elementRef: ElementRef) {  }

  ngOnInit() {
  this.elementRef.nativeElement.style.backgroundColor = '#fff';
  }
}
```

> In the component html

```
<button appExample>Button</button>
```

**Also there is a better way to create directive, as shown in below**

```
import { Directive, OnInit, ElementRef, Renderer2 } from '@angular/core'

@Directive({
  selector: '[appBetterExample]',
})
export class ExampleDirective implements OnInit {
  constructor(private elementRef: ElementRef, private renderer: Renderer2) {  }

  ngOnInit() {
  this.renderer.setStyle(this.elementRef.nativeElement, 'backgroundColor', '#fff')
  }
}
```

> In the component html

```
<button appBetterExample>Button</button>
```

Learn more about the available Renderer methods **[here.](https://angular.io/api/core/Renderer2)**

## **@HostListener() Decorator**

In Angular, the @HostListener() function decorator allows you to handle events of the host element in the directive class.

```
import { Directive, OnInit, ElementRef, Renderer2, HostListener  } from '@angular/core'

@Directive({
  selector: '[appBetterExample]',
})
export class ExampleDirective implements OnInit {
  constructor(private elementRef: ElementRef, private renderer: Renderer2) {  }

  ngOnInit() {
  }

  @HostListener('mouseover') onMouseOver() {
    this.ChangeBgColor('blue');
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.ChangeBgColor('red');
  }

  ChangeBgColor(color: string) {
this.renderer.setStyle(this.elementRef.nativeElement, 'backgroundColor', color)
  }
}
```

> In component.html

```
<div appBetterExample> Some thing </div>
```

In the above example at first the background color will be transparent when we hover over the div element backgroundColor will be blue.
And when the mouse moved away color will be red.
If we want red color initially call this.ChangeBgColor('red'); in ngOnInit().

## **@HostBinding() Decorator**

In Angular, the @HostBinding() function decorator allows you to set the properties of the host element from the directive class.

```
import { Directive, HostListener, HostBinding } from '@angular/core';

@Directive({
  selector: '[appBetterExample]'
})
export class BetterExampleDirective {
  @HostBinding('style.backgroundColor') backgroundColor: string   // if we want initial color we can assign here.

  constructor() {}

  @HostListener('mouseover') onMouseOver() {
    this.backgroundColor = 'blue';
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.backgroundColor = 'red';
  }
}
```

> In component.html

```
<div appBetterExample> Some thing </div>
```

Here also initially the bg color will be transparent, when we hover over the div element bg color will be blue and
when the mouse moved away bg color will be red.

## **Binding to directive property**

### **Method 1**:

```
import { Directive, HostListener, HostBinding, Input, OnInit } from '@angular/core';

@Directive({
  selector: '[appBetterExample]'
})
export class BetterExampleDirective implements OnInit {

  @Input() defaultColor: string = 'red';
  @Input() highlightColor: string = 'blue';

  @HostBinding('style.backgroundColor') backgroundColor: string;

  constructor() {}

  ngOnInit() {
    this.backgroundColor = this.defaultColor;
  }

  @HostListener('mouseover') onMouseOver() {
    this.backgroundColor = this.highlightColor;
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.backgroundColor = this.defaultColor;
  }
}
```

> In component.html

```
<div appBetterExample [defaultColor]="'yellow'" [highlightColor]="'orange'"> Some thing </div>
```

### **Method 2**:

```
import { Directive, HostListener, HostBinding, Input, OnInit } from '@angular/core';

@Directive({
  selector: '[appBetterExample]'
})
export class BetterExampleDirective implements OnInit {

  @Input() defaultColor: string = 'red';
  @Input('appBetterExample') highlightColor: string = 'blue';

  @HostBinding('style.backgroundColor') backgroundColor: string;

  constructor() {}

  ngOnInit() {
    this.backgroundColor = this.defaultColor;
  }

  @HostListener('mouseover') onMouseOver() {
    this.backgroundColor = this.highlightColor;
  }

  @HostListener('mouseleave') onMouseLeave() {
    this.backgroundColor = this.defaultColor;
  }
}
```

> In component.html

```
<div [appBetterExample]="'orange'" [defaultColor]="'yellow'"> Some thing </div>
```

In method 2 we are giving the selector of directive as an alias for @Input of highlightColor.
So that we can pass the heighlight color directly by binding the directive in html.

## **Creating custom structural directive**

Below is the directive that works similar as angular \*ngIF

```
import { Directive, Input, TemplateRef, ViewContainerRef } from '@angular/core';

@Directive({
  selector: '[myIf]'
})
export class MyIfDirective {

  @Input() set myIf(condition: boolean) {
    if (condition) {
      this.vcRef.createEmbeddedView(this.templateRef)
    } else {
      this.vcRef.clear();
    }

  }

  constructor(private templateRef: TemplateRef<any>, private vcRef: ViewContainerRef) { }

}
```

> In component.html

```
<div *ngIf="show" >Angular *ngIf</div>
<div *myIf="show" >My *myIf</div>
```

In the above example *myIf directive works same way as *ngIf.

## **Router Link**

```
<li role="presentation"><a [routerLink]="['/servers']">Servers</a></li>
<li role="presentation"><a routerLink="/users">Users</a></li>
```

Both the syntax are correct. But the 1st syntax will be useful when we have dynamic values to generate the link.
For detailed documentation [visit here](https://angular.io/api/router/RouterLink#description)

The syntax without `/` will work if we are in the parent component and navigating to Servers component.

```
<li role="presentation"><a [routerLink]="['servers']">Servers</a></li>
```

But if we are already in the Servers component and adding the relative path and clicking on this again will give error.

eg: if we are in the `localhost:4200/servers` then clicking on another routerLink `[routerLink]="['servers']"` from inside servers page will throw error.

```
<a [routerLink]="['servers']">Reload Server</a>
```

Because it will add `localhost:4200/servers/servers`.

### If we want to add some class when the link is active we can use routerLinkActive.

```
<a [routerLink]="['/servers']" routerLinkActive="active">Servers</a>
```

For more click [here](https://angular.io/api/router/RouterLinkActive#description)

-- Active route links cascade down through each level of the route tree, so parent and child router links can be active at the same time.
To override this behavior, you can bind to the [routerLinkActiveOptions] input binding with the { exact: true } expression. By using { exact: true },
a given RouterLink will only be active if its URL is an exact match to the current URL.

```
<a routerLink="/user" routerLinkActive="active-link" [routerLinkActiveOptions]="{exact:true}">Bob</a>
```

For more click [here](https://angular.io/api/router/RouterLinkActive#description)

### **Navigating programmatically**

```
 //in your constructor
 constructor(private router: Router){}

 onReloadClick() {
 //navigation link.
 this.router.navigate(['/servers']);
 }
```

### **To add relative path**

```
constructor( private route: ActivatedRoute) {}

onReloadClick() {
   this.router.navigate(['/servers'], {relativeTo: this.route});
 }
```

## **Fetching route parameters**

> In module .ts

```
const routes: Routes = [
 {path: 'users', component: UsersComponent},
 {path: 'users/:id/:name', component: UserComponent}

```

> In component.ts

```
export class UserComponent implements OnInit {
 user: {id: number, name: string};

 constructor(private route:ActivatedRoute) { }

 ngOnInit() {
   this.user = {
     id: this.route.snapshot.params['id'],
     name: this.route.snapshot.params['name']
   }
 }
}
```

> In component.html

```
<p>User with ID {{user.id}} loaded.</p>
<p>User name is {{user.name}}</p>
```

This is how the parameters are fetched from route.
But this will not work if we are already in the user component and we are updating the user route.
For that we need to fetch route reactively as shown below.

> In component.ts

```
export class UserComponent implements OnInit {
 user: {id: number, name: string};

 constructor(private route:ActivatedRoute) { }

 ngOnInit() {
   this.user = {
     id: this.route.snapshot.params['id'],
     name: this.route.snapshot.params['name']
   }
   this.route.params.subscribe((params: Params) => {
     this.user.id = params['id'];
     this.user.name = params['name'];
   });
 }
}
```

> In component.html

```
<p>User with ID {{user.id}} loaded.</p>
<p>User name is {{user.name}}</p>

<button class="btn btn-primary" [routerLink]="['/users', '10', 'Anna']">Anna (10)</button>
```

## **Query Parameters and Fragments**

### Adding query parameters and fragments using routerLink

> In routes

```
{path: 'servers/:id/edit', component: EditServerComponent},
```

> In component.html

```
 <a
    [routerLink]= "['/servers', '5', 'edit']"
    [queryParams]="{allowEdit: '1'}"
    [fragment]="'loading'"
    class="list-group-item"
    *ngFor="let server of servers">
    {{ server.name }}
</a>
```

### Adding query parameters and fragments programmatically (in ts)

> In component.html

```
<button class="btn btn-primary" (click)="onReloadClick(1)">Reload Server 1</button>
```

> In component.ts

```
onReloadClick(id:number) {
    this.router.navigate(['/servers', id, 'edit'], {queryParams: {allowEdit: '1'}, fragment: 'loading'} );
  }
```

### Retrieving query parameters and fragments

```
constructor(private route: ActivatedRoute) { }

ngOnInit() {
   console.log(this.route.snapshot.queryParams);
   console.log(this.route.snapshot.fragment);

   this.route.queryParams.subscribe();
   this.route.fragment.subscribe();
 }
```

Just like params query params we can subscribe and use.

## **Nested Route (child routes)**

```
const routes: Routes = [
  {path: '', component: HomeComponent},
  {path: 'users', component: UsersComponent, children: [
    {path: ':id/:name', component: UserComponent},
  ]},
  {path: 'servers', component: ServersComponent, children: [
    {path: ':id', component: ServerComponent},
    {path: ':id/edit', component: EditServerComponent},
  ]},
]
```

Now add `<router-outlet></router-outlet>` directive where you want to show the child components.

## **Handling query parameters**

If we want to preserve the queryParams that we set from one child component while navigating to another child
component we can use `queryParamsHandling: "preserve"`.
If we want to merge the queryParams with new queryParams we can use `queryParamsHandling: "merge"`.

```
this.router.navigate(['/edit'], queryParamsHandling: "preserve" });
```

For more visit [here.](https://angular.io/api/router/QueryParamsHandling)

## **Redirecting Routes**

```
{ path: '', redirectTo: '/somewhere-else', pathMatch: 'full' }
```

## **canActivate & canActivateChild**

```
 {path: 'servers',
  // canActivate: [AuthGuard],
  canActivateChild: [AuthGuard],
  component: ServersComponent,
  children: [
    {path: ':id', component: ServerComponent},
    {path: ':id/edit', component: EditServerComponent},
  ]},
```

To protect the route we can use canActivate and to protect the child route use canActivateChild.

## **CanDeactivate**

<center>⚠️ Work In Progress ⚠️</center>

## **Synchronous**

Synchronous code waits for one action to complete before moving to the next.

## **Asynchronous**

Asynchronous execution means that immediately after the client calls the method, it continues to execute the next JavaScript statement or
and when these results are returned a callback function is executed on the client according to certain conditions.

## **RXJS (Reactive Extensions for JavaScript)**

RxJS is a library for reactive programming which can be used to deal with asynchronous data streams.

## **Observables**

An Observable is an object that over time and asynchronously emits multiple data values (data stream).

- If we are not subscribing to the observable, so we do not receive the data.
- If we subscribe to the observable it will simply return the data.
- Observable is cancellable in nature by invoking unsubscribe() method.

```
const observable = new Observable((data) => {
data.next(1);
data.next(2);
data.next(3);
}).subscribe(element => console.log('Observable ' + element));
```

> Output

```
Observable 1
Observable 2
Observable 3
```

## **Promise**

- Promise returns the value regardless of then() method.
- Promise is not cancellable in nature.

```
const promise = new Promise((data) =>
	{ data(1);
	  data(2);
	  data(3); })
	.then(element => console.log(‘Promise ‘ + element));
```

> Output

```
Promise 1
```

## **Promise vs Observable**

As soon as a promise is made, the execution takes place. But Observables are lazy so nothing happens until a subscription is made.
While promises handle a single event, observable is a stream that allows passing of more than one event. A callback is made for each event in an observable.

## **Difference between find() and filter()**

### **find()**

- The find() method returns the first value that matches from the collection. Once it matches the value in findings,
  it will not check the remaining values in the array collection.<br/>
- Find return an object.

### **filter()**

- The filter() method returns the matched values in an array from the collection. It will check all values in the collection and return the matched values in an array.<br/>
- Filter returns an array.

---

<center>⚠️ Work In Progress ⚠️</center>

---

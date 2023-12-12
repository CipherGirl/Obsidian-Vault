**Components** in Angular determine **[[Views]]**, or screen elements. They interact with **[[Service]]** for tasks unrelated to views. By injecting these services as dependencies, code becomes modular and efficient. 

View: A component and its template together define a _view_. A component can contain a _view hierarchy_, which allows you to define arbitrarily complex areas of the screen that can be created, modified, and destroyed as a unit.

> Angular uses Components to build webpages, and uses modules to basically bundle different pieces into packages
> - Maximillan 

### Components Snippet

```ts
import { Component } from '@angular/core';

@Component({
  selector:    'app-hero-list',
  templateUrl: './hero-list.component.html',
  providers:  [ HeroService ]
})
export class HeroListComponent implements OnInit {
  /* . . . */
}
```

|CONFIGURATION OPTIONS|DETAILS|
|:--|:--|
|`selector`|A CSS selector that tells Angular to create and insert an instance of this component wherever it finds the corresponding tag in template HTML. For example, if an application's HTML contains `<app-hero-list></app-hero-list>`, then Angular inserts an instance of the `HeroListComponent` view between those tags.|
|`templateUrl`|The module-relative address of this component's HTML template. Alternatively, you can provide the HTML template inline, as the value of the `template` property. This template defines the component's _host view_.|
|`providers`|An array of [providers](https://angular.io/guide/glossary#provider) for services that the component requires. In the example, this tells Angular how to provide the `HeroService` instance that the component's constructor uses to get the list of heroes to display.|


### Fundamentals:

* [[Data Binding]]: 
	* Angular supports _two-way data binding_, a mechanism for coordinating the parts of a template with the parts of a component. Add binding markup to the template HTML to tell Angular how to connect both sides.
* [[Pipes]]

### Takeaways:
* A component is technically a directive.
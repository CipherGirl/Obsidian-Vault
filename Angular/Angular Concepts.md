Source: https://angular.io/guide/architecture#introduction-to-angular-concepts

Fundamentals: 
- [[Module]]: 
	- The basic building blocks of the Angular framework are Angular **Components** that are organized into **NgModules**. NgModules collect related code into functional sets; an Angular application is defined by a set of NgModules.
	  
- [[@Component]]: 
	- **Component** define _**Views**_, which are sets of screen elements that Angular can choose among and modify according to your program logic and data
	- Components use _**Services**_, which provide specific functionality not directly related to views. Service providers can be _injected_ into components as _dependencies_, making your code modular, reusable, and efficient.
	  
- [[Router]]: 
	- Angular provides the **Router** (https://angular.io/api/router/Router) service to help you define navigation paths among views. The router provides sophisticated in-browser navigational capabilities.
* [[Directive]]
	  
- [[Decorator]]: 
	- Modules, components and services are classes that use **_Decorator_**. These decorators mark their type and provide metadata that tells Angular how to use them. Example: `@Component`
- [[Lifecycle]]: 
- [[Others]]
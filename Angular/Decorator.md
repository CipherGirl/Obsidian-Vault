Decorators are functions that modify JavaScript classes. Decorators provide a way to add metadata to class declarations, which allows Angular to understand the intention and role of a class or property, and act accordingly.

In Angular, a decorator is a special kind of declaration that can be attached to classes, properties, methods, or parameters. Decorators use the form `@expression`, where `expression` must evaluate to a function that will be called at runtime with information about the decorated declaration.

1. **Class Decorators**:
    
    - `@NgModule`: Defines a module that contains components, directives, pipes, and providers.
    - `@Component`: Declares a class as an Angular component and provides configuration metadata.
    - `@Injectable`: Declares a class as injectable, allowing it to be used as a service or for dependency injection.
    - `@Directive`: Declares a class as a directive, which manipulates the DOM in some way.
      
2. **Property Decorators**:
    - `@Input()`: Declares a class property as an input property, which means data is passed from a parent component.
    - `@Output()`: Declares a class property as an output property, which can emit events to a parent component.
    - `@ViewChild() / @ViewChildren()`: Configures a view query, which can get the first or all child elements or directives from the view DOM.
    - `@HostBinding()`: Binds a host element property (from the component where this directive is defined on) to a directive property.
      
3. **Method Decorators**:
    - `@HostListener()`: Declares a DOM event to listen for and provides a handler method to run when that event occurs.
    
1. **Parameter Decorators**:
    - `@Inject()`: Provides a custom token for a parameter in a class constructor, allowing dependency injection.

Decorators are a key part of Angular's architecture, enabling the framework to understand how to instantiate, render, and link different classes and elements together. They are a feature of TypeScript and have been proposed for future versions of JavaScript as well.
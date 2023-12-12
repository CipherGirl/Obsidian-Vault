## Attribute Directives:

Attribute directives alter the appearance or behavior of an element, component, or another directive. They are applied to elements as attributes.

Many attribute directives are defined through modules such as the [`CommonModule`](https://angular.io/api/common/CommonModule), [`RouterModule`](https://angular.io/guide/router "Routing and Navigation") and [`FormsModule`](https://angular.io/guide/forms "Forms").

1. **`ngClass`:**
    - Syntax: `[ngClass]="{'class-name': expression}"`
    - Example: 
	```html
	<div [ngClass]="{'active': isActive, 'disabled': isDisabled}">Styled Content</div>
	```
    - Usage: Adds or removes CSS classes based on the truthiness of the expression.
      
2. **`ngStyle`:**
    - Syntax: `[ngStyle]="{'property': expression}"`
    - Example:
    ```html
	<div [ngStyle]="{'color': textColor, 'font-size': fontSize}">Styled Content</div>
	```
    - Usage: Sets inline styles based on the values of the provided expressions.
      
3. **`ngModel`:**
    - Syntax: `[(ngModel)]="property"`
    - Example: 
    ```html
    <input [(ngModel)]="name" />
```
    - Usage: Creates a two-way data binding on an input element, updating the property in the component.
      
4. **`ngDisabled`:**
    - Syntax: `[ngDisabled]="expression"`
    - Example: 
    ```html
    <button [ngDisabled]="isButtonDisabled">Click me</button>
```
    - Usage: Disables or enables an element based on the truthiness of the expression.


## Custom Attribute Directive

1. To create a directive, use the CLI command [`ng generate directive`](https://angular.io/cli/generate).
    
    `ng generate directive highlight`
    
    The CLI creates `src/app/highlight.directive.ts`, a corresponding test file `src/app/highlight.directive.spec.ts`, and declares the directive class in the `AppModule`.
    
    The CLI generates the default `src/app/highlight.directive.ts` as follows:
    
    src/app/highlight.directive.ts
    
	```js
	import {Directive} from '@angular/core';  
	@Directive({   
		standalone: true,   
		selector: '[appHighlight]', 
	}) 
	export class HighlightDirective {}
	```
    
    The `@Directive` decorator's configuration property specifies the directive's CSS attribute selector, `[appHighlight]`.
    
2. Import `ElementRef` from `@angular/core`. `ElementRef` grants direct access to the host DOM element through its `nativeElement` property.
    
3. Add `ElementRef` in the directive's `constructor()` to [inject](https://angular.io/guide/dependency-injection) a reference to the host DOM element, the element to which you apply `appHighlight`.
    
4. Add logic to the `HighlightDirective` class that sets the background to yellow.
    
    src/app/highlight.directive.ts
    
    ```js
    import { Directive, ElementRef } from '@angular/core';  
    @Directive({   
	    standalone: true,  
	    selector: '[appHighlight]', 
	}) 
	export class HighlightDirective {   
		constructor(private el: ElementRef) {     
			this.el.nativeElement.style.backgroundColor = 'yellow';   
		} 
	}
```

**N.B: Not ideal to access elements directly and  change the style. It can't accessed it if the DOM is not rendered because Angular can render templates without DOM**

```ts
import { Directive, ElementRef, OnInit, Renderer2 } from '@angular/core';  

@Directive({
	selector: '[appBetterHighlight]',
})

export class BetterHighlightDirective implements OnInit {
	constructor(private elementRef: ElementRef, private renderer: Renderer2) {}
	ngOnInit(): void {
		this.renderer.setStyle( this.elementRef.nativeElement, 
		'background-color', 'blue');
	}
}
```


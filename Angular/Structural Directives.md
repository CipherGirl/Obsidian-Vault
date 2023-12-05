Structural directives are responsible for shaping or altering the structure of the DOM by adding, removing, or manipulating elements. They are preceded by an asterisk (*) in the HTML template. 

<b>(*) is important.</b> 

**N.B: Can't use more than one structural directive on a single element in the template**

1. **`ngIf`:**
    - Syntax: `*ngIf="expression"`
    - Example: 
  ```html
	  <div *ngIf="isTrue">Content displayed when isTrue is true</div>
  ```
    - Usage: Conditionally renders or removes elements based on the truthiness of the expression.
      
2. **`ngFor`:**
    - Syntax: `*ngFor="let item of items"`
    - Example:
    ```html
    <li *ngFor="let item of items">{{ item }}</li>
    ```
    - Usage: Iterates over a collection (array) and repeats the host element for each item.
      
3. **`ngSwitch`:**
    - Syntax: `[ngSwitch]="expression"`
    - Example:
	```html
	<div [ngSwitch]="value">   
		<div *ngSwitchCase="'case1'">Content for case1</div>   
		<div *ngSwitchCase="'case2'">Content for case2</div>   
		<div *ngSwitchDefault>Default content</div> 
	</div>
	```
    - Usage: Switches among a set of cases based on the value of the expression.


### Attribute Directives:

Attribute directives alter the appearance or behavior of an element, component, or another directive. They are applied to elements as attributes.

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
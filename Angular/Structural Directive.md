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
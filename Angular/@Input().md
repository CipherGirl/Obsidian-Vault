Decorator that marks a class field as an input property and supplies configuration metadata. The input property is bound to a DOM property in the template. During change detection, Angular automatically updates the data property with the DOM property's value.

## [Options](https://angular.io/api/core/Input#options "Link to this heading")

|alias[](https://angular.io/api/core/Input#alias "Link to this heading")<br>|
|---|
|The name of the DOM property to which the input property is bound.|
|```alias?: string```|

|required[](https://angular.io/api/core/Input#required "Link to this heading")<br>|
|---|
|Whether the input is required for the directive to function.|
|```required?: boolean```|

|transform[](https://angular.io/api/core/Input#transform "Link to this heading")<br>|
|---|
|Function with which to transform the input value before assigning it to the directive instance.|
|```transform?: (value: any) => any```|

### Usage Notes
```ts
import { Component, Input, numberAttribute, booleanAttribute } from '@angular/core';
@Component({
  selector: 'bank-account',
  template: `
    Bank Name: {{bankName}}
    Account Id: {{id}}
    Account Status: {{status ? 'Active' : 'InActive'}}
  `
})
class BankAccount {
  // This property is bound using its original name.
  // Defining argument required as true inside the Input Decorator
  // makes this property deceleration as mandatory
  @Input({ required: true }) bankName!: string;
  // Argument alias makes this property value is bound to a different property name
  // when this component is instantiated in a template.
  // Argument transform convert the input value from string to number
  @Input({ alias:'account-id', transform: numberAttribute }) id: number;
  // Argument transform the input value from string to boolean
  @Input({ transform: booleanAttribute }) status: boolean;
  // this property is not bound, and is not automatically updated by Angular
  normalizedBankName: string;
}

@Component({
  selector: 'app',
  template: `
    <bank-account bankName="RBC" account-id="4747" status="true"></bank-account>
  `
})
class App {}
```
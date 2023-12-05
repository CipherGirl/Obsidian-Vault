A directive is a class with a `@Directive()` (https://angular.io/api/core/Directive) decorator.

_A component is technically a directive. However, components are so distinctive and central to Angular applications that Angular defines the `@Component()` decorator, which extends the `@Directive()` decorator with template-oriented features._

Types of Directives:
1. [[Structural Directives]] (Has the asterisk in front)
2. Attribute Directive
	1. Default (Provided by Angular)
	2. [[Custom Directive]]
ngModel - For 2 way data binding
A directive is a class with a `@Directive()` (https://angular.io/api/core/Directive) decorator.


The different types of Angular directives are as follows:

|DIRECTIVE TYPES|DETAILS|
|:--|:--|
|[ [[@Component]] ](https://angular.io/guide/component-overview)|Used with a template. This type of directive is the most common directive type.|
|[ [[Attribute Directive]] ](https://angular.io/guide/built-in-directives#built-in-attribute-directives)|Change the appearance or behavior of an element, component, or another directive.|
|[ [[Structural Directive]] ](https://angular.io/guide/built-in-directives#built-in-structural-directives)|Change the DOM layout by adding and removing DOM elements.|


_A component is technically a directive. However, components are so distinctive and central to Angular applications that Angular defines the `@Component()` decorator, which extends the `@Directive()` decorator with template-oriented features._

** **Both Structural and Attribute directives can be created by user these are *Custom Directives*

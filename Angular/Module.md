NgModules are cohesive code blocks in Angular dedicated to specific application areas or functionalities. They can encompass components, services, and other code, defining their scope. NgModules can both import features from other modules and export their own for use elsewhere.

Every Angular app has a primary `AppModule` in `app.module.ts`. Though small apps might have just this module, larger ones feature multiple modules, forming a hierarchical structure with `AppModule` at the root.

### NgModule Snippet

```ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
@NgModule({ // Decrotaor
  imports:      [ BrowserModule ],
  providers:    [ Logger ],
  declarations: [ AppComponent ],
  exports:      [ AppComponent ],
  bootstrap:    [ AppComponent ] // -> Root component
})
export class AppModule { }
```

### [NgModule Metadata](https://angular.io/guide/architecture-modules#ngmodule-metadata "Link to this heading")

An NgModule is defined by a class decorated with [@NgModule](https://angular.io/api/core/NgModule). The `@[NgModule]` decorator is a function that takes a single metadata object, whose properties describe the module. The most important properties are as follows.

|PROPERTIES|DETAILS|
|:--|:--|
|`declarations`|The [components](https://angular.io/guide/architecture-components), _directives_, and _pipes_ that belong to this NgModule.|
|`exports`|The subset of declarations that should be visible and usable in the _component templates_ of other NgModules.|
|`imports`|Other modules whose exported classes are needed by component templates declared in _this_ NgModule.|
|`providers`|Creators of [services](https://angular.io/guide/architecture-services) that this NgModule contributes to the global collection of services; they become accessible in all parts of the application. (You can also specify providers at the component level.)|
|`bootstrap`|The main application view, called the _root component_, which hosts all other application views. Only the _root NgModule_ should set the `bootstrap` property.|


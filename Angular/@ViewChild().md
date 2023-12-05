Property decorator that configures a view query. The change detector looks for the first element or the directive matching the selector in the view DOM. If the view DOM changes, and a new child matches the selector, the property is updated.

## Description[](https://angular.io/api/core/ViewChild#description "Link to this heading")

**Metadata Properties**:

- **selector** - The directive type or the name used for querying.
- **read** - Used to read a different token from the queried elements.
- **static** - `true` to resolve query results before change detection runs, `false` to resolve after change detection. Defaults to `false`.
The following selectors are supported.

- Any class with the @[Component](https://angular.io/api/core/Component) or @[Directive](https://angular.io/api/core/Directive) decorator
- A template reference variable as a string (e.g. query `<my-component #cmp></my-component>` with `@ViewChild('cmp'))
- Any provider defined in the child component tree of the current component (e.g. `@ViewChild someService: SomeService`)
- Any provider defined through a string token (e.g. `@ViewChild someTokenVal: any`)
- A [TemplateRef](https://angular.io/api/core/TemplateRef) (e.g. query `<ng-template></ng-template>` with `@ViewChild (TemplateRef template;`)

```ts
import {Component, Directive, Input, ViewChild} from '@angular/core';

@Directive({selector: 'pane'})
export class Pane {
  @Input() id!: string;
}

@Component({
  selector: 'example-app',
  template: `
    <pane id="1" *ngIf="shouldShow"></pane>
    <pane id="2" *ngIf="!shouldShow"></pane>

    <button (click)="toggle()">Toggle</button>

    <div>Selected: {{selectedPane}}</div>
  `,
})
export class ViewChildComp {
  @ViewChild(Pane)
  set pane(v: Pane) {
    setTimeout(() => {
      this.selectedPane = v.id;
    }, 0);
  }
  selectedPane: string = '';
  shouldShow = true;
  toggle() {
    this.shouldShow = !this.shouldShow;
  }
}
```

Decorator that marks a DOM property or an element class, style or attribute as a host-binding property and supplies configuration metadata. Angular automatically checks host bindings during change detection, and if a binding changes it updates the host element of the directive.

|Option|Description|
|---|---|
|[`hostPropertyName?`](https://angular.io/api/core/HostBinding#hostPropertyName)|The DOM property that is bound to a data property. This field also accepts:<br><br>- classes, prefixed by `class.`<br>- styles, prefixed by `style.`<br>- attributes, prefixed by `attr.`|

## Usage notes[](https://angular.io/api/core/HostBinding#usage-notes "Link to this heading")

The following example creates a directive that sets the `valid` and `invalid` class, a style color, and an id on the DOM element that has an [ngModel](https://angular.io/api/forms/NgModel) directive on it.

```ts
@Directive({selector: '[ngModel]'})
class NgModelStatus {
  constructor(public control: NgModel) {}
  // class bindings
  @HostBinding('class.valid') get valid() { return this.control.valid; }
  @HostBinding('class.invalid') get invalid() { return this.control.invalid; }

  // style binding
  @HostBinding('style.color') get color() { return this.control.valid ? 'green': 'red'; }

  // style binding also supports a style unit extension
  @HostBinding('style.width.px') @Input() width: number = 500;

  // attribute binding
  @HostBinding('attr.aria-required')
  @Input() required: boolean = false;

  // property binding
  @HostBinding('id') get id() { return this.control.value?.length ? 'odd':  'even'; }

@Component({
  selector: 'app',
  template: `<input [(ngModel)]="prop">`,
})
class App {
  prop;
}
```


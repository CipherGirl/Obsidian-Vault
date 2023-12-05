Decorator that declares a DOM event to listen for, and provides a handler method to run when that event occurs.

|Option|Description|
|---|---|
|[`eventName?`](https://angular.io/api/core/HostListener#eventName)|The DOM event to listen for.|
|[`args?`](https://angular.io/api/core/HostListener#args)|A set of arguments to pass to the handler method when the event occurs.|

## Description[](https://angular.io/api/core/HostListener#description "Link to this heading")

Angular invokes the supplied handler method when the host element emits the specified event, and updates the bound element with the result.

If the handler method returns false, applies `preventDefault` on the bound element.

## Usage notes[](https://angular.io/api/core/HostListener#usage-notes "Link to this heading")

The following example declares a directive that attaches a click listener to a button and counts clicks.

```ts
@Directive({selector: 'button[counting]'})
class CountClicks {
  numberOfClicks = 0;

  @HostListener('click', ['$event.target'])
  onClick(btn) {
    console.log('button', btn, 'number of clicks:', this.numberOfClicks++);
  }
  
  @HostListener('mouseenter') mouseover(eventData: Event) {
	this.renderer.setStyle(this.elementRef.nativeElement, 'background-color',
	'blue');
  }
  @HostListener('mouseleave') mouseleave(eventData: Event) {
	this.renderer.setStyle(this.elementRef.nativeElement,
	'background-color','transparent');
  }
}

@Component({
  selector: 'app',
  template: '<button counting>Increment</button>',
})
class App {}
```

Angular supports _two-way data binding_, a mechanism for coordinating the parts of a template with the parts of a component. Add binding markup to the template HTML to tell Angular how to connect both sides.

There are two types of data binding:

|DATA BINDINGS|DETAILS|
|:--|:--|
|[Event Binding](https://angular.io/guide/event-binding)|Lets your application respond to user input in the target environment by updating your application data.|
|[Property Binding](https://angular.io/guide/property-binding)|Lets you interpolate values that are computed from your application data into the HTML.|

![[Data Binding.png]] 

![[Screenshot from 2023-11-28 17-05-51.png]]

## Property Binding:
With `[]` we define the property binding in HTML level.

## Event Binding:
With `()` we define the event binding in HTML level.

## Two Way Binding:
Property Binding + Event Binding = `[()]`
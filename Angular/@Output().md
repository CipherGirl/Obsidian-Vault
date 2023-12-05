Decorator that marks a class field as an output property and supplies configuration metadata. The DOM property bound to the output property is automatically updated during change detection.

|Option|Description|
|---|---|
|[`alias?`](https://angular.io/api/core/Output#alias)|The name of the DOM property to which the output property is bound.|

## Options[](https://angular.io/api/core/Output#options "Link to this heading")

|alias[](https://angular.io/api/core/Output#alias "Link to this heading")|
|---|
|The name of the DOM property to which the output property is bound.|
|```<br>alias?: string<br>```|

## Usage notes[](https://angular.io/api/core/Output#usage-notes "Link to this heading")

You can supply an optional name to use in templates when the component is instantiated, that maps to the name of the bound property. By default, the original name of the bound property is used for output binding.

See [Input](https://angular.io/api/core/Input) decorator for an example of providing a binding name.
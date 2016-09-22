# ir-native-input-reflector

**Polymer 1.0 control to enable custom web component submission as a field in a native html &lt;form&gt;.**

You might have been puzzled about how exactly a non-native component may be submitted as part of a static form. 
You might also be aware that it's not possibble to append child elements to input elements. 
Thus it's not possible to enrich an input with shadow dom.

ir-native-input-reflector is a presentationless element solves this by adding a hidden native input to its lite dom, reflecting the 
targetField property of its target to the hidden field. The `name` of the hidden input field is determined by the host's `.name` property.
The update is done upon `.changeEvent` which defaults to `'change'`.
The hidden input is thus submitted as part of the native form under the given name, and provides the developer with
an element that feels totally like any input element. 

## How it works
- In the `attached` lifecycle phase a hidden input element is created in the ir-native-input-reflector's Light DOM.
- When `changeEvent` event fires, `valueAttr` of the source element is reflected to the hidden native input element's `value` attribute. You may optionally specify a mapping from specific values matched as regex to specific values e.g. `map="[{ "^ever" : "xxx" }]"` will map all values starting with 'ever' to value 'xxx'.
- Ninja mode: use multiple sources (source="id1,id2,i3,...") and .operator to combine values of multiple controls. In this case `.map` is ignored.

## Usage

    <ir-native-input-reflector name="isPublished" value-attr="checked" on-event="iron-change" map='[{ "false" : "0" }, {"." : "true"}]'></ir-native-input-reflector>

| property 	    | type 		| description |
| ------------- | --------- | ----------- |
| source	    | String	| id of target element to reflect. if not provided will try to match by `name`. |
| name		    | String 	| Specifies input name that will be submitted as part of the form. if not provided will attempt to use target element's `name`, if that's not available will be useless. |
| valueAttr     | String	| value attr to reflect from source element (e. g. 'checked', 'value'). Default is 'value'. |
| changeEvent	| String	| event on source element that triggers updates. Default: `'change'`|
| map 		    | Object 	| json map of regex=>value mappings, e.g.: '[{ "false" : "0"}, { "attr" : "@[value]" }, {"." : "true"}]'. First match wins. Keeps the value intact when empty or no match. Use @[attr-name] to interpolate with attr value from source element. |
| operation	    | String	| ninja mode - currently can only take values "add" for arithmetic addition and "concat" for string concatenation |
| operationOptions	| Object	| { concatString : <string to use when 'concat' option is used, skip : <regex, skip matching values (applied after map)> } |
	
## Related
This control complements [ir-reflect-to-native-behavior](https://github.com/IgorRubinovich/ir-reflect-to-native-behavior), which may
be used by web components developers to enable submission of components as part of a native html form. ir-reflect-to-native-behavior is
great for bringing native form compliance to new components that developer has control over. ir-native-input-reflector on the other hand
works with 3rd party components the developer does not control.
Please see [ir-reflect-to-native-behavior](https://github.com/IgorRubinovich/ir-reflect-to-native-behavior) for more details.

## To-do
- Demo

## Changelist
- v0.55 added transformations on multiple sources [ninja mode]

## License
[MIT](http://opensource.org/licenses/MIT) 

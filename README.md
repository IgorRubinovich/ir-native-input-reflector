# ir-native-input-reflector

**Polymer 1.0 behavior to enable custom web component submission as a field in a native html form.**

You might have been puzzled about how exactly a non-native component may be submitted as part of a static form. 
You might also be aware that it's not possibble to append child elements to input elements. 
Thus it's not possible to enrich an input with shadow dom.

ir-native-input-reflector is a presentationless element solves this by adding a hidden native input to its lite dom, reflecting the 
targetField property of its target to the hidden field. The name of the hidden input field is determined by the host's .name property. 
The hidden input is thus submitted as part of the native form under the given name, and provides the developer with
an element that feels totally like any input element.

## How it works
- In the `attached` lifecycle phase a hidden input element is created in the ir-native-input-reflector's Light DOM.
- A two-way bound `.value` property is added to the host. When the host updates `.value`.
it is reflected to the hidden native input element's `value` attribute.

## Usage

    <ir-native-input-reflector name="isPublished" value-attr="checked" on-event="iron-change" map='[{ "false" : "0" }, {"." : "true"}]'></ir-native-input-reflector>

	| property 	| type 		| description |
	| -------- 	| --------- | ----------- |
	| name		| String 	| Specifies input name that will be submitted as part of the form. if not provided will attempt to use target element's name, if that's not available will be useless |
	| target	| String	| id of target element to reflect. if not provided will try to match by name |
	| valueAttr | String	| value attr to reflect from target element (e. g. 'checked', 'value'). Default is `value`. |
	| onEvent	| String	| event on source element that triggers updates |
	| map 		| Object 	| json map of regex=>value mappings, e.g.: '[{ "false" : "0"}, {"." : "true"}]'. First match wins. Keeps the value intact when empty or no match. |

	
## Related
This control complements [ir-reflect-to-native-behavior](https://github.com/IgorRubinovich/ir-reflect-to-native-behavior), which may
be used by web components developers to enable submission of components as part of a native html form. ir-reflect-to-native-behavior is
great for bringing native form compliance to new components that developer has control over. ir-native-input-reflector on the other hand
works with 3rd party components the developer does not control.
Please see [ir-reflect-to-native-behavior](https://github.com/IgorRubinovich/ir-reflect-to-native-behavior) for more details.

## To-do
- Demo

## License
[MIT](http://opensource.org/licenses/MIT) 

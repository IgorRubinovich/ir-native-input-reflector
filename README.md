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

- Simple: Assign to `.value` when host's "output" value changes and don't worry about the rest.
- Advanced: Observe `.value` to update host's internal state.

## To-do
- Demo

## License
[MIT](http://opensource.org/licenses/MIT) 

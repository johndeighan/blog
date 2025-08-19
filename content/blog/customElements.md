Custom Elements
===============

```coffee
class MyCustomElement extends HTMLElement

	@observedAttributes = ['size']

	constructor: () ->
		super()
		@_internals = @attachInternals()

	# --- Element functionality written in here

	connectedCallback: () ->
		console.log "Custom element added to page."

	disconnectedCallback: () ->
		console.log "Custom element removed from page."

	adoptedCallback: () ->
		console.log "Custom element moved to new page."

	attributeChangedCallback: (name, oldValue, newValue) ->
		console.log "Attribute #{name} has changed."

	isCollapsed: () ->
		return @_internals.states.has('collapsed')

	collapse: () ->
		@_internals.states.add('collapsed')
		return

	expand: () ->
		@_internals.states.delete('collapsed')
		return

customElements.define "my-custom-element", MyCustomElement
```

You can now use CSS like this:

```css
my-custom-element {
	border: dashed red;
	}
my-custom-element:state(hidden) {
	border: none;
	}
```

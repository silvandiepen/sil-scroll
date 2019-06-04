# Scroll

A simple Vue Directive add a function of an element when the browser scrolls. 


### Install

Install the package
`npm install @sil/scroll`


Import the package

`import Scroll from '~/@sil/scroll`

Define the component:

```js
	Vue.directive(Scroll);
```

Use the component with default values:

```html
<any-element v-scroll />	
```


#### Arguments

| Argument  | Default   | Description                                                                                                               |
| --------- | --------- | ------------------------------------------------------------------------------------------------------------------------- |
| fn        | undefined | When you want to pass custom argument, you need to set you callback function on `fn`                                      |
| active    | true      | Wether or not the directive should be initiated. False can be handy during debugging.                                     |
| immidiate | true      | The function set on the scroll will be triggered on initialisation of the directive by default.                           |
| element   | window    | The scroll event listener will be set on the window by default, but can also be set on the element itself by using 'this' |

#### Callback

the function you use, will be given back the event and the element its using. `(event, element)`

#### Example Usage

This function can for instance be set on an element to check where it is on the page. Based on that you can set classes or do anything else.

```html
	<template>
		<div class="container">
			<section v-scroll="handleScroll" ></section>
			<section v-scroll="handleScroll" ></section>
			<section v-scroll="handleScroll" ></section>
			<section v-scroll="handleScroll" ></section>
		</div>
	</template>
```

```js
export default{
	methods: {
		handleScroll(evt, el) {
			// Just get it once per call.
		 	const rect = el.getBoundingClientRect();

			// This just checks if the element is above the fold and its bottom is under it.
			if (rect.top <= 0 && (rect.top + rect.height) > 0) {
				// Do something tho this element.
			}
	}
}

```


#### Example with custom arguments

```html
<template>
	<div class="container">
		<section v-scroll="{fn: handleScroll, immediate: false" ></section>
		 // Function will be the same but not immediately invoked.
	</div>
</template>
```
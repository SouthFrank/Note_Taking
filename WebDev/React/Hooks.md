### State Hooks

### Effect Hooks

> The Effect Hook lets you perform side effects on function components. Data fetching, setting up a subscription, and manually changing the DOM in React components are all examples of side effects.

#### useEffect

The most popular effect hook, useEffect connects a component to an external system.
![[Pasted image 20240109095256.png]]

Effect hooks are commonly used when making http requests with axios. Example:
![[Pasted image 20240109100006.png]]

- The function useEffect takes two parameters:
	- The first is a function, the *effect* itself
	- The second parameter is used to specify how often the effect is run. 
		- By default, the effect is always run after the component has been rendered. If the second parameter is an empty array `[]` like in the above example, then the effect is only run along with the first render of the component.
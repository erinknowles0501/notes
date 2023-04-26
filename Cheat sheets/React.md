## Atomic + composable focused
React seems especially focused on very small atoms (eg: a Button with Text and Icon components) and is definitely focused on composition - props don't re-render unless they change, so passing components as props (either as children or defined props) can help with performance.

## Hooks
### useState
 - Good for internal logic state - can be passed around a bit with props if need be but should be used just for state that the component needs to operate - whether a modal is open, for example.
### useEffect
 - Triggered when the watched value changed. This is an *escape hatch*, for synchronizing React with something external (eg updating the window title when the SPA page changes) - if you're using an effect for something internal, that's a code smell. You can probably instead use a component key, or calculate during render, or restructure somehow.
### useContext
 - Used to pass data 'down through' levels of child components. Can be modified as it goes down, so any children of the modifier get modified state, but parents don't. This means that in addition to **scoped app state**, it's also handy for **recursive/nested components**.
### useReducer
 - takes a state and an action - action modifies the state and returns the state. Important that the reducer function is pure - no side effects, same input always gives same output. 
 - Can use with useContext to pass the state down through components.

## Nested state is a pain
In React, state is technically immutable, so the whole state object is replaced when anything changes. For example, to change something nested:

```
function handleTitleChange(e) {
    setPerson({
	    ...person,
	    artwork: {
	        ...person.artwork,
	        title: e.target.value
	    }
    });
}
```

This becomes kind of infuriating. There's a lib called Immer that abstracts away a lot of this (generates the above from `person.artwork.title = 'New title'`). React docs recommend 'flattening' state - for example, instead of storing the artwork on the person, store the id of the artwork, and then map it.

## Redux
Developed the reducer pattern.
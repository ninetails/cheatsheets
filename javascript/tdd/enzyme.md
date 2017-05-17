# Enzyme

## React Wrapper

```js
wrap = shallow(<MyComponent />) // => ReactWrapper (shallow)
wrap = mount(<MyComponent />)   // => ReactWrapper (full)
```

### Transversing

```js
wrap.find('button')   // => ReactWrapper
wrap.filter('button') // => ReactWrapper
wrap.not('span')      // => ReactWrapper (inverse of filter())
wrap.children()       // => ReactWrapper
wrap.parent()         // => ReactWrapper
wrap.closest('div')   // => ReactWrapper
wrap.childAt(0)       // => ReactWrapper
wrap.at(0)            // => ReactWrapper
wrap.first()          // => ReactWrapper
wrap.last()           // => ReactWrapper
```

```js
wrap.get(0)           // => ReactElement
wrap.getNode()        // => ReactElement
wrap.getNodes()       // => Array<ReactElement>
wrap.getDOMNode()     // => DOMComponent
```

### Actions

```js
wrap.simulate('click')
```

### React components

```js
wrap.setState({ ... })
wrap.setProps({ ... })
wrap.setContext({ ... })

wrap.state()            // => Any (get state)
wrap.props()            // => object (get props)
wrap.context()          // => Any (get context)

wrap.instance()         // => ReactComponent
```

### Mount

```js
wrap.mount()
wrap.unmount()
wrap.update()      // calls forceUpdate()
```

### Tests

```js
wrap.debug()               // => string
wrap.html()                // => string
wrap.text()                // => string
wrap.type()                // => string | function
wrap.name()                // => string
wrap.is('.classname')      // => boolean
wrap.hasClass('class')     // => boolean
wrap.exists()              // => boolean
wrap.contains(<div />)     // => boolean
wrap.contains([ <div /> ]) // => boolean

wrap.containsMatchingElement(<div />)         // => boolean
wrap.containsAllMatchingElements([ <div /> ]) // => boolean
wrap.containsAnyMatchingElements([ <div /> ]) // => boolean
```

## Enzyme Render Docs

### [Selector](https://github.com/airbnb/enzyme/blob/master/docs/api/selector.md)

#### A Valid CSS Selector

- class syntax (`.foo`, `.foo-bar`, etc.)
- tag syntax (`input`, `div`, `span`, etc.)
- id syntax (`#foo`, `#foo-bar`, etc.)
- prop syntax (`[htmlFor="foo"]`, `[bar]`, `[baz=1]`, etc.);

Enzyme supports combining any of those supported syntaxes

    div.foo.bar
    input#input-name
    label[foo=true]

Also the following contextual selectors

    .foo .bar
    .foo > .bar
    .foo + .bar
    .foo ~ .bar
    .foo input

#### A React Component Constructor

```js
class MyComponent extends React.Component {
  render() { ... }
}

// find instances of MyComponent
const myComponents = wrapper.find(MyComponent);
```

#### A React Component's displayName

```js
class MyComponent extends React.Component {
  render() { ... }
}
MyComponent.displayName = 'MyComponent';

// find instances of MyComponent
const myComponents = wrapper.find('MyComponent');
```

#### Object Property selector

```js
const wrapper = mount(
  <div>
    <span foo={3} bar={false} title="baz" />
  </div>
)

wrapper.find({ foo: 3 })
wrapper.find({ bar: false })
wrapper.find({ title: 'baz'})
```

### [shallow - ShallowWrapper API](https://github.com/airbnb/enzyme/blob/master/docs/api/shallow.md)

#### [`.find(selector) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/find.md)
Find every node in the render tree that matches the provided selector.

#### [`.findWhere(predicate) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/findWhere.md)
Find every node in the render tree that returns true for the provided predicate function.

#### [`.filter(selector) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/filter.md)
Remove nodes in the current wrapper that do not match the provided selector.

#### [`.filterWhere(predicate) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/filterWhere.md)
Remove nodes in the current wrapper that do not return true for the provided predicate function.

#### [`.contains(nodeOrNodes) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/contains.md)
Returns whether or not a given node or array of nodes is somewhere in the render tree.

#### [`.containsMatchingElement(node) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/containsMatchingElement.md)
Returns whether or not a given react element exists in the shallow render tree.

#### [`.containsAllMatchingElements(nodes) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/containsAllMatchingElements.md)
Returns whether or not all the given react elements exists in the shallow render tree.

#### [`.containsAnyMatchingElements(nodes) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/containsAnyMatchingElements.md)
Returns whether or not one of the given react elements exists in the shallow render tree.

#### [`.equals(node) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/equals.md)
Returns whether or not the current render tree is equal to the given node, based on the expected value.

#### [`.matchesElement(node) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/matchesElement.md)
Returns whether or not a given react element matches the shallow render tree.

#### [`.hasClass(className) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/hasClass.md)
Returns whether or not the current node has the given class name or not.

#### [`.is(selector) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/is.md)
Returns whether or not the current node matches a provided selector.

#### [`.exists() => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/exists.md)
Returns whether or not the current node exists.

#### [`.isEmpty() => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/isEmpty.md)
*Deprecated*: Use [.exists()](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/exists.md) instead.

#### [`.not(selector) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/not.md)
Remove nodes in the current wrapper that match the provided selector. (inverse of `.filter()`)

#### [`.children() => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/children.md)
Get a wrapper with all of the children nodes of the current wrapper.

#### [`.childAt(index) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/childAt.md)
Returns a new wrapper with child at the specified index.

#### [`.parents() => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/parents.md)
Get a wrapper with all of the parents (ancestors) of the current node.

#### [`.parent() => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/parent.md)
Get a wrapper with the direct parent of the current node.

#### [`.closest(selector) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/closest.md)
Get a wrapper with the first ancestor of the current node to match the provided selector.

#### [`.shallow([options]) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/shallow.md)
Shallow renders the current node and returns a shallow wrapper around it.

#### [`.render() => CheerioWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/render.md)
Returns a CheerioWrapper of the current node's subtree.

#### [`.unmount() => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/unmount.md)
A method that un-mounts the component.

#### [`.text() => String`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/text.md)
Returns a string representation of the text nodes in the current render tree.

#### [`.html() => String`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/html.md)
Returns a static HTML rendering of the current node.

#### [`.get(index) => ReactElement`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/get.md)
Returns the node at the provided index of the current wrapper.

#### [`.getNode() => ReactElement`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/getNode.md)
Returns the wrapper's underlying node.

#### [`.getNodes() => Array<ReactElement>`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/getNodes.md)
Returns the wrapper's underlying nodes.

#### [`.at(index) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/at.md)
Returns a wrapper of the node at the provided index of the current wrapper.

#### [`.first() => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/first.md)
Returns a wrapper of the first node of the current wrapper.

#### [`.last() => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/last.md)
Returns a wrapper of the last node of the current wrapper.

#### [`.state([key]) => Any`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/state.md)
Returns the state of the root component.

#### [`.context([key]) => Any`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/context.md)
Returns the context of the root component.

#### [`.props() => Object`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/props.md)
Returns the props of the current node.

#### [`.prop(key) => Any`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/prop.md)
Returns the named prop of the current node.

#### [`.key() => String`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/key.md)
Returns the key of the current node.

#### [`.simulate(event[, data]) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/simulate.md)
Simulates an event on the current node.

#### [`.setState(nextState) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/setState.md)
Manually sets state of the root component.

#### [`.setProps(nextProps) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/setProps.md)
Manually sets props of the root component.

#### [`.setContext(context) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/setContext.md)
Manually sets context of the root component.

#### [`.instance() => ReactComponent`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/instance.md)
Returns the instance of the root component.

#### [`.update() => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/update.md)
Calls `.forceUpdate()` on the root component instance.

#### [`.debug() => String`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/debug.md)
Returns a string representation of the current shallow render tree for debugging purposes.

#### [`.type() => String|Function`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/type.md)
Returns the type of the current node of the wrapper.

#### [`.name() => String`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/name.md)
Returns the name of the current node of the wrapper.

#### [`.forEach(fn) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/forEach.md)
Iterates through each node of the current wrapper and executes the provided function

#### [`.map(fn) => Array`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/map.md)
Maps the current array of nodes to another array.

#### [`.reduce(fn[, initialValue]) => Any`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/reduce.md)
Reduces the current array of nodes to a value

#### [`.reduceRight(fn[, initialValue]) => Any`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/reduceRight.md)
Reduces the current array of nodes to a value, from right to left.

#### [`.slice([begin[, end]]) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/slice.md)
Returns a new wrapper with a subset of the nodes of the original wrapper, according to the rules of `Array#slice`.

#### [`.tap(intercepter) => Self`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/tap.md)
Taps into the wrapper method chain. Helpful for debugging.

#### [`.some(selector) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/some.md)
Returns whether or not any of the nodes in the wrapper match the provided selector.

#### [`.someWhere(predicate) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/someWhere.md)
Returns whether or not any of the nodes in the wrapper pass the provided predicate function.

#### [`.every(selector) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/every.md)
Returns whether or not all of the nodes in the wrapper match the provided selector.

#### [`.everyWhere(predicate) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/everyWhere.md)
Returns whether or not all of the nodes in the wrapper pass the provided predicate function.

#### [`.dive([options]) => ShallowWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ShallowWrapper/dive.md)
Shallow render the one non-DOM child of the current wrapper, and return a wrapper around the result.

### [mount - ReactWrapper API](https://github.com/airbnb/enzyme/blob/master/docs/api/mount.md)

#### [`.find(selector) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/find.md)
Find every node in the render tree that matches the provided selector.

#### [`.findWhere(predicate) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/findWhere.md)
Find every node in the render tree that returns true for the provided predicate function.

#### [`.filter(selector) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/filter.md)
Remove nodes in the current wrapper that do not match the provided selector.

#### [`.filterWhere(predicate) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/filterWhere.md)
Remove nodes in the current wrapper that do not return true for the provided predicate function.

#### [`.contains(nodeOrNodes) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/contains.md)
Returns whether or not a given node or array of nodes is somewhere in the render tree.

#### [`.containsMatchingElement(node) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/containsMatchingElement.md)
Returns whether or not a given react element is somewhere in the render tree.

#### [`.containsAllMatchingElements(nodes) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/containsAllMatchingElements.md)
Returns whether or not all the given react elements are somewhere in the render tree.

#### [`.containsAnyMatchingElements(nodes) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/containsAnyMatchingElements.md)
Returns whether or not one of the given react elements is somewhere in the render tree.

#### [`.hasClass(className) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/hasClass.md)
Returns whether or not the current root node has the given class name or not.

#### [`.is(selector) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/is.md)
Returns whether or not the current node matches a provided selector.

#### [`.exists() => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/exists.md)
Returns whether or not the current node exists.

#### [`.isEmpty() => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/isEmpty.md)
*Deprecated*: Use [.exists()](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/exists.md) instead.

#### [`.not(selector) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/not.md)
Remove nodes in the current wrapper that match the provided selector. (inverse of `.filter()`)

#### [`.children() => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/children.md)
Get a wrapper with all of the children nodes of the current wrapper.

#### [`.childAt() => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/childAt.md)
Returns a new wrapper with child at the specified index.

#### [`.parents() => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/parents.md)
Get a wrapper with all of the parents (ancestors) of the current node.

#### [`.parent() => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/parent.md)
Get a wrapper with the direct parent of the current node.

#### [`.closest(selector) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/closest.md)
Get a wrapper with the first ancestor of the current node to match the provided selector.

#### [`.render() => CheerioWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/render.md)
Returns a CheerioWrapper of the current node's subtree.

#### [`.text() => String`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/text.md)
Returns a string representation of the text nodes in the current render tree.

#### [`.html() => String`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/html.md)
Returns a static HTML rendering of the current node.

#### [`.get(index) => ReactElement`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/get.md)
Returns the node at the provided index of the current wrapper.

#### [`.getNode() => ReactElement`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/getNode.md)
Returns the wrapper's underlying node.

#### [`.getNodes() => Array<ReactElement>`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/getNodes.md)
Returns the wrapper's underlying nodes.

#### [`.getDOMNode() => DOMComponent`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/getDOMNode.md)
Returns the outer most DOMComponent of the current wrapper.

#### [`.at(index) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/at.md)
Returns a wrapper of the node at the provided index of the current wrapper.

#### [`.first() => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/first.md)
Returns a wrapper of the first node of the current wrapper.

#### [`.last() => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/last.md)
Returns a wrapper of the last node of the current wrapper.

#### [`.state([key]) => Any`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/state.md)
Returns the state of the root component.

#### [`.context([key]) => Any`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/context.md)
Returns the context of the root component.

#### [`.props() => Object`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/props.md)
Returns the props of the root component.

#### [`.prop(key) => Any`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/prop.md)
Returns the named prop of the root component.

#### [`.key() => String`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/key.md)
Returns the key of the root component.

#### [`.simulate(event[, mock]) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/simulate.md)
Simulates an event on the current node.

#### [`.setState(nextState) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/setState.md)
Manually sets state of the root component.

#### [`.setProps(nextProps) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/setProps.md)
Manually sets props of the root component.

#### [`.setContext(context) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/setContext.md)
Manually sets context of the root component.

#### [`.instance() => ReactComponent`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/instance.md)
Returns the instance of the root component.

#### [`.unmount() => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/unmount.md)
A method that un-mounts the component.

#### [`.mount() => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/mount.md)
A method that re-mounts the component.

#### [`.update() => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/update.md)
Calls `.forceUpdate()` on the root component instance.

#### [`.debug() => String`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/debug.md)
Returns a string representation of the current render tree for debugging purposes.

#### [`.type() => String|Function`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/type.md)
Returns the type of the current node of the wrapper.

#### [`.name() => String`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/name.md)
Returns the name of the current node of the wrapper.

#### [`.forEach(fn) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/forEach.md)
Iterates through each node of the current wrapper and executes the provided function

#### [`.map(fn) => Array`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/map.md)
Maps the current array of nodes to another array.

#### [`.matchesElement(node) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/matchesElement.md)
Returns whether or not a given react element matches the current render tree.

#### [`.reduce(fn[, initialValue]) => Any`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/reduce.md)
Reduces the current array of nodes to a value

#### [`.reduceRight(fn[, initialValue]) => Any`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/reduceRight.md)
Reduces the current array of nodes to a value, from right to left.

#### [`.slice([begin[, end]]) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/slice.md)
Returns a new wrapper with a subset of the nodes of the original wrapper, according to the rules of `Array#slice`.

#### [`.tap(intercepter) => Self`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/tap.md)
Taps into the wrapper method chain. Helpful for debugging.

#### [`.some(selector) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/some.md)
Returns whether or not any of the nodes in the wrapper match the provided selector.

#### [`.someWhere(predicate) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/someWhere.md)
Returns whether or not any of the nodes in the wrapper pass the provided predicate function.

#### [`.every(selector) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/every.md)
Returns whether or not all of the nodes in the wrapper match the provided selector.

#### [`.everyWhere(predicate) => Boolean`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/everyWhere.md)
Returns whether or not all of the nodes in the wrapper pass the provided predicate function.

#### [`.ref(refName) => ReactWrapper`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/ref.md)
Returns a wrapper of the node that matches the provided reference name.

#### [`.detach() => void`](https://github.com/airbnb/enzyme/blob/master/docs/api/ReactWrapper/detach.md)
Unmount the component from the DOM node it's attached to.

## Render Methods

`shallow` vs `mount` vs `render` lifecycle methods

### Bar.js

```js
import React from 'react';

function Bar() {
    return (
      <div>
        Hello world,
        <span>
          we&apos;re not testing Bar so this would ideally not executed
          through either shallow rendering or Jest&apos;s auto mocking.
        </span>
      </div>
    );
}

export default Bar;
```

### Foo.js

```js
import React, { Component } from 'react';
import Bar from './Bar';

class Foo extends Component {

    constructor(props) {
        console.log('constructor');
        super(props);
        this.state = {
            foo: 'bar'
        };
    }

    componentWillMount() {
        console.log('componentWillMount');
    }

    componentDidMount() {
        console.log('componentDidMount');
    }

    componentWillReceiveProps() {
        console.log('componentWillReceiveProps');
    }

    shouldComponentUpdate() {
        console.log('shouldComponentUpdate');
        return true;
    }

    componentWillUpdate() {
        console.log('componentWillUpdate');
    }

    componentDidUpdate() {
        console.log('componentDidUpdate');
    }

    componentWillUnmount() {
        console.log('componentWillUnmount');
    }

    render() {
        console.log('render');
        return (
            <div>
                Hello Foo
                <Bar foo="bar"></Bar>
            </div>
        );
    }

}

export default Foo;
```

### Foo.test.js

```js
jest.unmock('./Foo');

import React from 'react';
import { shallow, mount, render } from 'enzyme';
import { renderIntoDocument } from 'react-addons-test-utils';
import Foo from './Foo';
import Bar from './Bar';

// Jest automocking doesn't work right away with stateless components, i.e. you have to force
// them to return a renderable value.
// As it turns out state*full* components only work because of a hack in React:
// https://github.com/facebook/react/blob/6b1232aa86415f0573153888a46c4c5cb38974d8/src/renderers/shared/stack/reconciler/ReactCompositeComponent.js#L1103
Bar.mockImplementation(() => <div className="button" />); // React 0.14
// Bar.mockImplementation(() => null); // React 15

Error.stackTraceLimit = 10;

describe('components/Foo', () => {
  describe('rendering methods', () => {
    it('Shallow Rendering - shallow', () => {
      console.log('Shallow Rendering - shallow');
      // constructor
      // componentWillMount
      // render
      // setProps()
      // componentWillReceiveProps
      // shouldComponentUpdate
      // componentWillUpdate
      // render
      const wrapper = shallow(<Foo />);
      console.log('setProps()');
      wrapper.setProps({
          foo: 'bar'
      });
      console.log(wrapper.debug());
    });

    it('Full DOM Rendering - mount', () => {
      console.log('Full DOM Rendering - mount');
      // constructor
      // componentWillMount
      // render
      // componentDidMount
      // setProps()
      // componentWillReceiveProps
      // shouldComponentUpdate
      // componentWillUpdate
      // render
      // componentDidUpdate
      const wrapper = mount(<Foo />);
      console.log('setProps()');
      wrapper.setProps({
          foo: 'bar'
      });
      const button = wrapper.find(Button);
      expect(button.prop('foo')).toBe('bar');
      console.log(wrapper.debug());

      // const wasIstDas = renderIntoDocument(<Foo />);
      // console.log(wasIstDas); // ReactComponentTree?
    });

    it('Static Rendering API - render', () => {
      console.log('Static Rendering API - render');
      // constructor
      // componentWillMount
      // render
      const wrapper = render(<Foo />);
      console.log(wrapper.html()); // wrapper === Cheerio instance
    });
  });
});
```

## References

* [Rico Sta. Cruz Enzyme Cheatsheet](http://ricostacruz.com/cheatsheets/enzyme.html)
* [Render Methods](https://gist.github.com/richardscarrott/d89b37aff55ccc504193335198e676d1)

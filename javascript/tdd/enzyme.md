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

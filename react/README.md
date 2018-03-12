# The React Playbook

## Table of Contents

1.  [Coding Style](#coding-style)
1.  [Build Process](#build-process)
1.  [App Structure & Layout](#app-structure--layout)
1.  [Unit Testing](#unit-testing)
1.  [UI Library](#ui-library)
1.  [Data Fetching](#data-fetching)
1.  [State Management](#state-management)
1.  [CSS Style](#css-style)
1.  [Type Checking](#type-checking)

## Coding Style

Our coding style is enforced from a tool called Prettier. This tool will auto-format your code correctly based on the react community style guidelines. For a list of the rules this enforces [please see this link](https://github.com/yannickcr/eslint-plugin-react#list-of-supported-rules)

To install Prettier choose your IDE below and follow the instructions to "Format on Save":

* [VS Code](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)
* [Atom](https://atom.io/packages/prettier-atom)

### Class vs `React.createClass` vs stateless

* If you have internal state and/or refs, prefer `class extends React.Component` over `React.createClass`. eslint: [`react/prefer-es6-class`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-es6-class.md) [`react/prefer-stateless-function`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-stateless-function.md)

  ```jsx
  // bad
  const Listing = React.createClass({
    // ...
    render() {
      return <div>{this.state.hello}</div>;
    }
  });

  // good
  class Listing extends React.Component {
    // ...
    render() {
      return <div>{this.state.hello}</div>;
    }
  }
  ```

  And if you don't have state or refs, prefer normal functions (not arrow functions) over classes:

  ```jsx
  // bad
  class Listing extends React.Component {
    render() {
      return <div>{this.props.hello}</div>;
    }
  }

  // bad (relying on function name inference is discouraged)
  const Listing = ({ hello }) => <div>{hello}</div>;

  // good
  function Listing({ hello }) {
    return <div>{hello}</div>;
  }
  ```

### Naming

* **Extensions**: Use `.jsx` extension for React components.
* **Filename**: Use PascalCase for filenames. E.g., `ReservationCard.jsx`.
* **Reference Naming**: Use PascalCase for React components and camelCase for their instances. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

  ```jsx
  // bad
  import reservationCard from "./ReservationCard";

  // good
  import ReservationCard from "./ReservationCard";

  // bad
  const ReservationItem = <ReservationCard />;

  // good
  const reservationItem = <ReservationCard />;
  ```

* **Component Naming**: Use the filename as the component name. For example, `ReservationCard.jsx` should have a reference name of `ReservationCard`. However, for root components of a directory, use `index.jsx` as the filename and use the directory name as the component name:

  ```jsx
  // bad
  import Footer from "./Footer/Footer";

  // bad
  import Footer from "./Footer/index";

  // good
  import Footer from "./Footer";
  ```

* **Higher-order Component Naming**: Use a composite of the higher-order component's name and the passed-in component's name as the `displayName` on the generated component. For example, the higher-order component `withFoo()`, when passed a component `Bar` should produce a component with a `displayName` of `withFoo(Bar)`.

  > Why? A component's `displayName` may be used by developer tools or in error messages, and having a value that clearly expresses this relationship helps people understand what is happening.

  ```jsx
  // bad
  export default function withFoo(WrappedComponent) {
    return function WithFoo(props) {
      return <WrappedComponent {...props} foo />;
    }
  }

  // good
  export default function withFoo(WrappedComponent) {
    function WithFoo(props) {
      return <WrappedComponent {...props} foo />;
    }

    const wrappedComponentName = WrappedComponent.displayName
      || WrappedComponent.name
      || 'Component';

    WithFoo.displayName = `withFoo(${wrappedComponentName})`;
    return WithFoo;
  }
  ```

* **Always define explicit defaultProps for all non-required props.**

  > Why? propTypes are a form of documentation, and providing defaultProps means the reader of your code doesn’t have to assume as much. In addition, it can mean that your code can omit certain type checks.

  ```jsx
  // bad
  function SFC({ foo, bar, children }) {
    return (
      <div>
        {foo}
        {bar}
        {children}
      </div>
    );
  }
  SFC.propTypes = {
    foo: PropTypes.number.isRequired,
    bar: PropTypes.string,
    children: PropTypes.node
  };

  // good
  function SFC({ foo, bar, children }) {
    return (
      <div>
        {foo}
        {bar}
        {children}
      </div>
    );
  }
  SFC.propTypes = {
    foo: PropTypes.number.isRequired,
    bar: PropTypes.string,
    children: PropTypes.node
  };
  SFC.defaultProps = {
    bar: "",
    children: null
  };
  ```

### Ordering

Ordering for `class extends React.Component`:

1.  optional `static` methods
1.  `constructor`
1.  `getChildContext`
1.  `componentWillMount`
1.  `componentDidMount`
1.  `componentWillReceiveProps`
1.  `shouldComponentUpdate`
1.  `componentWillUpdate`
1.  `componentDidUpdate`
1.  `componentWillUnmount`
1.  _clickHandlers or eventHandlers_ like `onClickSubmit()` or `onChangeDescription()`
1.  _getter methods for `render`_ like `getSelectReason()` or `getFooterContent()`
1.  _optional render methods_ like `renderNavigation()` or `renderProfilePicture()`
1.  `render`

* How to define `propTypes`, `defaultProps`, `contextTypes`, etc...

  ```jsx
  import React from "react";
  import PropTypes from "prop-types";

  const propTypes = {
    id: PropTypes.number.isRequired,
    url: PropTypes.string.isRequired,
    text: PropTypes.string
  };

  const defaultProps = {
    text: "Hello World"
  };

  class Link extends React.Component {
    static methodsAreOk() {
      return true;
    }

    render() {
      return (
        <a href={this.props.url} data-id={this.props.id}>
          {this.props.text}
        </a>
      );
    }
  }

  Link.propTypes = propTypes;
  Link.defaultProps = defaultProps;

  export default Link;
  ```

Ordering for `React.createClass`: eslint: [`react/sort-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/sort-comp.md)

1.  `displayName`
1.  `propTypes`
1.  `contextTypes`
1.  `childContextTypes`
1.  `mixins`
1.  `statics`
1.  `defaultProps`
1.  `getDefaultProps`
1.  `getInitialState`
1.  `getChildContext`
1.  `componentWillMount`
1.  `componentDidMount`
1.  `componentWillReceiveProps`
1.  `shouldComponentUpdate`
1.  `componentWillUpdate`
1.  `componentDidUpdate`
1.  `componentWillUnmount`
1.  _clickHandlers or eventHandlers_ like `onClickSubmit()` or `onChangeDescription()`
1.  _getter methods for `render`_ like `getSelectReason()` or `getFooterContent()`
1.  _optional render methods_ like `renderNavigation()` or `renderProfilePicture()`
1.  `render`

## Build Process

Our build process relies on [Webpack](https://github.com/webpack/webpack/_) to transpile our assets (jsx, js, sass, etc) into a proper converted files for browsers. We rely on [BabelJS](https://babeljs.io/) to write ES2015+ JS, [PostCSS](http://postcss.org/) to autoprefix CSS and [ESLint](https://eslint.org/) to lint for errors.

Available Build commands are:

* `yarn run start` : The default command that runs `yarn run dev`
* `yarn run dev` : Build assets for local development, the default webpack option
* `yarn run build` : Build assets for production, adds UglifyJS and additonal options
* `yarn run test` : Run Jest tests.

**[⬆ back to top](#table-of-contents)**

## App Structure & Layout

```
project
│   package.json
│   webpack.config.js
│
└───client
│   │   componentRenderer.jsx
│   │
│   └───components
│   │   │
│   │   └───button
│   │       │   button.jsx
│   │       │   button.scss
│   │       │   button.test.jsx
│   │       │   ...
│   │
│   └───configs
│   │   │   polyfills.js
│   │   │   ...
│   │
│   └───containers
│   │   │   withAnalytics.jsx
│   │   │   ...
│   │
│   └───feature1
│       │   feat1.jsx
│       │   ...
│
└───public
│   │
│   └───dist
│       │   common.bbd96658a571118f01e5.js
│       │   main.bbd96658a571118f01e5.js
│       │   ...
```

**[⬆ back to top](#table-of-contents)**

## Unit Testing

For unit testing, we are using [Jest](https://facebook.github.io/jest/) with [Enzyme](https://github.com/airbnb/enzyme)
You can always run all the unit tests by doing:
* `yarn run`

[Shallow rendering](https://github.com/airbnb/enzyme/blob/master/docs/api/shallow.md) is useful to constrain yourself to testing a component as a unit, and to ensure that your tests aren't indirectly asserting on behavior of child components

Shallow rendering renders only component itself without its children. So if you change something in a child component it won’t change shallow output of your component. Or a bug, introduced to a child component, won’t break your component’s test. It also doesn’t require DOM.

For example this component:

```
const ButtonWithIcon = ({icon, children}) => (
    <button><Icon icon={icon} />{children}</button>
);
```
Will be rendered by React like this:
```
<button>
    <i class="icon icon_coffee"></i>
    Hello Jest!
</button>
```
But like this with shallow rendering:
```
<button>
    <Icon icon="coffee" />
    Hello Jest!
</button>
```
Note that the Icon component was not rendered.

Testing basic component rendering

That’s enough for most non-interactive components:
```
test('render a label', () => {
    const wrapper = shallow(
        <Label>Hello Jest!</Label>
    );
    expect(wrapper).toMatchSnapshot();
});

test('render a small label', () => {
    const wrapper = shallow(
        <Label small>Hello Jest!</Label>
    );
    expect(wrapper).toMatchSnapshot();
});

test('render a grayish label', () => {
    const wrapper = shallow(
        <Label light>Hello Jest!</Label>
    );
    expect(wrapper).toMatchSnapshot();
});
```

Full Example:

```jsx
import React from 'react';
import { configure, shallow } from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';
import Button from './button.jsx';

configure({ adapter: new Adapter() });

describe('Button', () => {
    let props;
    let mountedButton;
    const mountButton = () => {
        if (!mountedButton) {
            mountedButton = shallow(<Button {...props} />);
        }
        return mountedButton;
    };

    beforeEach(() => {
        props = {
            text: 'Default text',
            onClick: undefined,
        };
        mountedButton = undefined;
    });

    it('always renders a button', () => {
        const btn = mountButton().find('button');
        expect(btn.length).toEqual(1);
    });

    describe('when `text` is defined', () => {
        beforeEach(() => {
            props.text = 'Click me';
        });

        it('sets the button text', () => {
            const btn = mountButton()
                .find('button')
                .first();
            expect(btn.text()).toEqual('Click me');
        });
    });
});
```


**[⬆ back to top](#table-of-contents)**

## UI Library

WIP

**[⬆ back to top](#table-of-contents)**

## Data Fetching

* Use the [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) for making asynchronous network requests. Be sure to implement polyfills for any supported browsers that are not compatible.

* Use [Redux Thunk](https://github.com/gaearon/redux-thunk) to abstract network logic out of UI components.

**[⬆ back to top](#table-of-contents)**

## State Management

* Use [Redux](https://redux.js.org/) to manage state in React applications.

  > Why? Redux offers a predictable mechanism to store and mutate complex application state. The tooling provides an excellent developer experience, and the architecture encourages testability.

### Redux Actions

* Use the [Flux Standard Action](https://github.com/redux-utilities/flux-standard-action) format for structuring Redux actions. In brief:

  An action MUST

  * be a plain JavaScript object.
  * have a type property.

  An action MAY

  * have an error property.
  * have a payload property.
  * have a meta property.

  An action MUST NOT include properties other than type, payload, error, and meta.

* Always use an object for the payload property

  ```
  // bad
  dispatch({
      type: DELETE_TODO,
      payload: '1',
  });

  // good
  dispatch({
      type: DELETE_TODO,
      payload: {
          todoId: '1',
      },
  });
  ```

* Always define action types as string constants:

  ```
  // bad
  dispatch({
      type: 'LOAD_DATA',
  });

  // good
  const LOAD_DATA = 'LOAD_DATA';

  dispatch({
      type: LOAD_DATA,
  });
  ```

### Global Object Cache

* Use [Redux-ORM](https://github.com/tommikaikkonen/redux-orm) to manage relational data. Cached objects should never be duplicated on the client, regardless of how the REST responses are structured. This will cut down on memory footprint and make global updates much easier. Keep UI state separate from relational data.

  **Learn More:**

  * [Normalizing State Shape](https://redux.js.org/recipes/structuring-reducers/normalizing-state-shape)
  * [Updating Normalized Data](https://redux.js.org/recipes/structuring-reducers/updating-normalized-data)
  * [Practical Redux](http://blog.isquaredsoftware.com/2016/10/practical-redux-part-1-redux-orm-basics/)
  * [Redux-ORM API Docs](http://tommikaikkonen.github.io/redux-orm/index.html)

**[⬆ back to top](#table-of-contents)**

## CSS Style

The element returned by the `render` method should have a `className` matching the name of the component (or otherwise identifying the component). This is useful for "namespacing" any CSS/SASS that go with the component. For example:

```jsx
// Foobar.js
import React from "react";
import "foobar.scss";

class Greeting extends React.Component {
  render() {
    return <div className="foobar">Foobar</div>;
  }
}

export default Foobar;
```

```scss
// Foobar.scss
.foobar {
  // Rules defined here will only apply to Foobar elements
}
```

**[⬆ back to top](#table-of-contents)**

## Type Checking

For our type checking we are using [PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html).

PropTypes exports a range of validators that can be used to make sure the data you receive is valid. In this example, we’re using PropTypes.string. When an invalid value is provided for a prop, a warning will be shown in the JavaScript console. For performance reasons, propTypes is only checked in development mode.

```jsx
import PropTypes from "prop-types";

const propTypes = {
  name: PropTypes.string
};

const defaultProps = {
  text: "World"
};

class Greeting extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

Greeting.propTypes = propTypes;
Greeting.defaultProps = defaultProps;

export default Greeting;
```

**[⬆ back to top](#table-of-contents)**

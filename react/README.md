# The React Playbook

## Table of Contents

1.  [Coding Style](#coding-style)
1.  [Build Process](#build-process)
1.  [App Structure & Layout](#app-structure--layout)
1.  [Unit Testing](#unit-testing)
1.  [UI Library](#ui-library)
1.  [Data Fetching](#data-fetching)
1.  [Global State Management](#global-state-management)
1.  [CSS Style](#css-style)
1.  [Type Checking](#type-checking)

## Coding Style

WIP

**[⬆ back to top](#table-of-contents)**

## Build Process

Our build process relies on [Webpack](https://github.com/webpack/webpack/_) to transpile our assets (jsx, js, sass, etc) into a proper converted files for browsers. We rely on [BabelJS](https://babeljs.io/) to write ES2015+ JS, [PostCSS](http://postcss.org/) to autoprefix CSS and [ESLint](https://eslint.org/) to lint for errors.

Available Build commands are:

* `yarn run start` : The default command that runs `yarn run dev`
* `yarn run dev` : Build assets for local development, the default webpack option
* `yarn run build` : Build assets for production, adds UglifyJS and additonal options
* `yarn run test` : Run Jest tests.

**[⬆ back to top](#table-of-contents)**

## App Structure & Layout

WIP

**[⬆ back to top](#table-of-contents)**

## Unit Testing

WIP

**[⬆ back to top](#table-of-contents)**

## UI Library

WIP

**[⬆ back to top](#table-of-contents)**

## Data Fetching

WIP

**[⬆ back to top](#table-of-contents)**

## Global State Management

WIP

**[⬆ back to top](#table-of-contents)**

## CSS Style

WIP

**[⬆ back to top](#table-of-contents)**

## Type Checking

For our type checking we are using [PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html).

PropTypes exports a range of validators that can be used to make sure the data you receive is valid. In this example, we’re using PropTypes.string. When an invalid value is provided for a prop, a warning will be shown in the JavaScript console. For performance reasons, propTypes is only checked in development mode.

```
import PropTypes from 'prop-types';

class Greeting extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}

Greeting.propTypes = {
  name: PropTypes.string
};
```

**[⬆ back to top](#table-of-contents)**

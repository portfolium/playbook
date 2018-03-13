# The AngularJS Playbook

## Table of Contents

1.  [Coding Style](#coding-style)
1.  [Build Process](#build-process)
1.  [App Structure & Layout](#app-structure--layout)
1.  [Unit Testing](#unit-testing)
1.  [UI Library](#ui-library)
1.  [Data Fetching](#data-fetching)
1.  [Global State Management](#global-state-management)
1.  [Type Checking](#type-checking)

## Coding Style

We loosely follow John Papa's AngularJS style guide. We've deviated in a few areas so we can't attempt to follow it 100%. We've also incorporated some of the principles of the Angular (version 2+) style guide in an attempt at easing the migration process in the future.

Todd Motto has created a great resource that's been kept up-to-date with best practices for Angular 1.6 with one-way data flow, components, etc. We've pieced together our Angular style from these two sources, so there is no definitive style guide resource at this time.

**[View the John Papa guide](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md)**

**[View the Todd Motto guide](https://github.com/toddmotto/angular-styleguide)**

**[⬆ back to top](#table-of-contents)**

## Build Process

WIP

**[⬆ back to top](#table-of-contents)**

## App Structure & Layout

We're still in the process of migrating the web project to a full single page app. Below you'll find the current structure as well as the proposed future structure.

### Current Structure

```
<project-root>
|-- application (php)
    ...
|-- assets
    ...
|-- client (angular)
    |-- components
        |-- feature-1
        |-- feature-2
        |-- feature-3
    |-- feature
        |-- js
            |-- action
            |-- component
            |-- config
            |-- constant
            |-- controller
            |-- directive
            |-- filter
            |-- model
            |-- reducer
            |-- service
        |-- sass
            |-- <partials>
            |-- <component-name>
            ...
        |-- template
            |-- <partials>
            |-- <component-name>
            ...
        index.js
        index.scss
    |-- layout
        |-- js
        |-- sass
        |-- template
        app.js
        app-legacy.js
        app-spa.js
    |-- main
        |-- sass
            ...
        index.scss
    |-- vendor
        ...
|-- gulpfile.js
    ...
|-- public
    |-- assets
        |-- build
            ...
    ...
|-- tests
    ...
...
```

### Proposed Structure

```
<project-root>
|-- dist
    ...
|-- e2e
    ...
|-- src
    |-- app
        |-- core (WIP)
            |-- config
            |-- directives
            |-- filters
            |-- services
            core.module.js
        |-- feature
            |-- sub-feature
                sub-feature.action.js
                sub-feature.component.html|js|scss|spec
                sub-feature.reducer.js|spec
            feature.action.js
            feature.component.html|js|scss
            feature.module.js
            feature.reducer.js|spec
            feature.routing.js
        |-- shared
            |-- feature-1
            |-- feature-2
            |-- feature-3
            ...
            shared.module.js
        app.module.js
        app.routing.js
    |-- assets
        ...
    |-- sass
        ...
    index.html
    main.js
...
```

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

## Type Checking

WIP

**[⬆ back to top](#table-of-contents)**

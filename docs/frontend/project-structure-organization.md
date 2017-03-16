Following the introduction of `.component()` in Angular 1.5, our front-end code has shifted toward a component-based architecture. This was a calculated move to help ease the transition to Angular 2, but the previous code structure conventions are no longer 100% applicable. In an effort to continue the move to component architecture and bring conventions in line with the new [Angular 2 Style Guide](https://angular.io/styleguide) we should re-think the organization of our code.

Below is an outline of how our code is structured now, and how it should be organized once the web project is a standalone Angular client. We will still use [folder by feature](https://angular.io/styleguide#!#04-07) organization but we'll put a larger emphasis on grouping component js, sass, and templates together.

## Current Structure
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

## Proposed Structure

Here is the new proposed structure. Share your feedback in the dev channel!

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

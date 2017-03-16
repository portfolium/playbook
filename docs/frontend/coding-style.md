## Javascript

Airbnb has done an excellent job compiling a practical style guideline for modern javascript. We've forked the project so we can modify it slightly to suit our needs (4 spaces ftw). Whenever an argument over style arises, consult the guide first. You can also configure [eslint](http://eslint.org/) to [enforce the style guide](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc) -- we'll be doing this for all new projects moving forward.

**[View the Javascript style guide](https://github.com/portfolium/javascript)**

## Angular

We loosely follow John Papa's AngularJS style guide. We've deviated in a few areas so we can't attempt to follow it 100%. We've also incorporated some of the principles of the Angular (version 2+) style guide in an attempt at easing the migration process in the future.

Todd Motto has created a great resource that's been kept up-to-date with best practices for Angular 1.6 with one-way data flow, components, etc. We've pieced together our Angular style from these two sources, so there is no definitive style guide resource at this time.

**[View the John Papa guide](https://github.com/johnpapa/angular-styleguide/blob/master/a1/README.md)**

**[View the Todd Motto guide](https://github.com/toddmotto/angular-styleguide)**

## Templates

We don't yet have a formalized guideline to follow for HTML templates, other than the HTML5 spec. More to come.

## Stylesheets

### Tooling

Stylesheets should be written and compiled using [Sass](http://sass-lang.com/) in the `.scss` syntax. [PostCSS](http://postcss.org/) is used to automate the addition of vendor prefixes, so they should be omitted from the codebase.

### Layouts

Complex layouts should be constructed using the flex box model. In AngularJS projects, we use the [Angular Material layout directives](https://material.angularjs.org/latest/layout/introduction) to assist in creating flex layouts. [flex-layout](https://github.com/angular/flex-layout) can be used to do the same in Angular projects. We don't yet have a good solution for non AngularJS/Angular projects.

### Methodology

We've adopted [BEM](https://css-tricks.com/bem-101/) as our stylesheet methodology of choice. We loved BEM for its simplicity and declarative nature. BEM forces you to stop and think about breaking your styles into smaller, more re-usable pieces by limiting the level of nesting in stylesheets.

**[View the BEM style guide](http://getbem.com/introduction/)**

### Organization

For component-based applications, stylesheets should be self-contained and imported directly into the component files. Global, application-wide styles should be grouped logically by folder and imported into a single `app.scss` file.

### Design Core

A shared sass library project is currently in progress at [design-core](https://github.com/portfolium/design-core) to share variables, mixins, and common styles across projects. [design-core](https://github.com/portfolium/design-core) is also a living style guide, shipping auto generated documentation alongside the source code. It will follow SemVer so changes can be incorporated into projects at their own pace.

We will slowly migrate pieces of the main web project into design-core, ensuring each piece that gets migrated is properly documented.

**[View the design-core project](https://github.com/portfolium/design-core)**


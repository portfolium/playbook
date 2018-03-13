# The Frontend Playbook

## Table of Contents

1.  [Javascript](#javascript)
1.  [CSS](#css)
1.  [HTML](#html)

## Javascript

* Follow the [Portfolium Javascript Styleguide](https://github.com/portfolium/javascript), which we've forked from Airbnb's comprehensive javascript styleguide.

* [Enforce the style guide](https://github.com/airbnb/javascript/blob/master/linters/.eslintrc) using [eslint](http://eslint.org/)

**[⬆ back to top](#table-of-contents)**

## CSS

### Pre/Post Processors

* Write styles using [Sass](http://sass-lang.com/) in the `.scss` syntax

* Use [PostCSS](http://postcss.org/) to automate the addition of vendor prefixes, and other

### Layouts

* Construct complex layouts using the flex box model.

### Methodology

* Follow [BEM](https://css-tricks.com/bem-101/) best practices for structuring styles.

  > Why? BEM forces you to stop and think about breaking your styles into smaller, more re-usable pieces by limiting the level of nesting in stylesheets.

  **Resources:**

  * [Introduction to BEM](http://getbem.com/introduction/)

### Design Core

* Import shared sass variables and mixins from the Portfolium [design-core](https://github.com/portfolium/design-core) library.

  > Why? To reduce duplicate code and implement the [Design System](https://portfolium.design) across all of our products and services.

**[⬆ back to top](#table-of-contents)**

## HTML

We don't yet have a formalized guideline to follow for HTML templates, other than the HTML5 spec. More to come.

**[⬆ back to top](#table-of-contents)**

#Jetthoughts CSS/SASS Style Guide
_In our guide we combine rules from [AIRBNB](https://github.com/airbnb/css) style guide and [RSCSS](http://rscss.io/) naming conventions. Advanced rules can be taken from links above, else is presented in current guide._

## Components and Elements
- All elements should be decomposed by the components. Each component should be placed in their own file. 
- Components should be named with at least two words, separated by a dash `-` . [More..](http://rscss.io/components.html)
- Each component may have elements. They should have classes that are only one word. [More..](http://rscss.io/elements.html)
- Components and elements may have a variants. Variants should be wrapped wit a separate class and will be prefixed with a dash `-`. [More..](http://rscss.io/variants.html)

##[File structure](http://www.sitepoint.com/architecture-sass-project/)
  How we might organize style files 
  ```
  stylesheets/ 
  | 
  |– base/ 
  |   |– _reset.scss       # Reset/normalize 
  |   |– _typography.scss  # Typography rules 
  |   ...                  # Etc… 
  | 
  |– components/ 
  |   |– _buttons.scss     # Buttons 
  |   |– _carousel.scss    # Carousel 
  |   |– _cover.scss       # Cover 
  |   |– _dropdown.scss    # Dropdown 
  |   |– _navigation.scss  # Navigation 
  |   ...                  # Etc… 
  | 
  |– helpers/ 
  |   |– _variables.scss   # Sass Variables 
  |   |– _functions.scss   # Sass Functions 
  |   |– _mixins.scss      # Sass Mixins 
  |   |– _helpers.scss     # Class & placeholders helpers 
  |   ...                  # Etc… 
  | 
  |– layout/ 
  |   |– _grid.scss        # Grid system 
  |   |– _header.scss      # Header 
  |   |– _footer.scss      # Footer 
  |   |– _sidebar.scss     # Sidebar 
  |   |– _forms.scss       # Forms 
  |   ...                  # Etc… 
  | 
  |– pages/ 
  |   |– _home.scss        # Home specific styles 
  |   |– _contact.scss     # Contact specific styles 
  |   ...                  # Etc… 
  | 
  |– themes/ 
  |   |– _theme.scss       # Default theme 
  |   |– _admin.scss       # Admin theme 
  |   ...                  # Etc… 
  | 
  |– vendors/ 
  |   |– _bootstrap.scss   # Bootstrap 
  |   |– _jquery-ui.scss   # jQuery UI 
  |   ...                  # Etc… 
  | 
  | 
  – main.scss             # primary Sass file
  ``` 
   
## [CSS](https://github.com/airbnb/css#css)
- Use soft tabs (2 spaces) for indentation
- Prefer dashes over camelCasing in class names. 
- Use classnames whenever possible. Tag selectors are fine, but they may come at a small performance penalty and may not be as descriptive.
- Do not use ID selectors
- When using multiple selectors in a rule declaration, give each selector its own line.
- Put a space before the opening brace `{` in rule declarations
- In properties, put a space after, but not before, the : character.
- Put closing braces `}` of rule declarations on a new line
- Put blank lines between rule declarations

## [Sass](https://github.com/airbnb/css#sass)
- Use `.scss`  format instead of `.sass`
- Order your @extend, regular CSS and @include declarations logically ([More...](https://github.com/airbnb/css#ordering-of-property-declarations))

## [Nested selectors](https://github.com/airbnb/css#nested-selectors)
- Do not nest selectors more than three levels deep! If it's necessary here are some [guidelines](http://rscss.io/nested-components.html) for doing that.

## [JavaScript in Css](https://github.com/airbnb/css#javascript-hooks)
- Avoid binding to the same class in both your CSS and JavaScript. Please create JavaScript-specific classes to bind to, prefixed with `.js-`

## [Layouts](http://rscss.io/layouts.html)
* Components should be made in a way that they're reusable in different contexts. Avoid putting these properties in components:
  * Positioning (position, top, left, right, bottom)
  * Floats (float, clear)
  * Margins (margin)
  * Dimensions (width, height) *

[More information](http://rscss.io/layouts.html)

## [Mixins](https://github.com/airbnb/css#mixins)
- Mixins, defined via @mixin and called with @include, should be used sparingly and only when function arguments are necessary. A mixin without function arguments (i.e. `@mixin hide { display: none; }`) is better accomplished using a placeholder selector ([More...](https://github.com/airbnb/css#placeholders)) in order to prevent code duplication.

## [Helpers](http://rscss.io/helpers.html)
- For general-purpose classes meant to override values, put them in a separate file and name them beginning with an underscore. They are typically things that are tagged with `!important`. Use them very sparingly.

## Purpose: Remind myself what I learn in SCSS

1. Two CSS preprocessors to choose from:
    - [Less](https://lesscss.org/) - JavaScript
    - [Sass](https://sass-lang.com/) - Ruby On Rail

1. Sass has two syntaxes avail:
    - Sass (Syntactically Awesome SytleSheets) in .sass files - indentations
    - SCSS (Sassy CSS) in .scss files - syntax more closely to CSS

1. Remember:
    - Sass is the name of the preprocessor
    - SCSS is more similar to CSS and easier to learn
    - all resources online mention Sass, not SCSS
    - all features are available for both systaxes
    - everything in SCSS is available in Sass
    - a CSS file is a valid SCSS file - compatibility  
    - difference between Sass and SCSS is [subtle](https://sass-lang.com/documentation/syntax).
&nbsp;  
&nbsp;  

## SCSS Features:
### Everything about Sass/SCSS is to provide tools for **DRY**
---
> ### [VARIABLES: prevents repeating values](https://marksheet.io/sass-variables.html)
- no more searching and replacing all occurrences of the same CSS value
- `#fce473 (css)` => `$yellow: #fce473 (.scss)`
- prepend variable with `$` to defining a variable
- .scss file will be compiled into a .css file, where all variables will be replaced with their actual values
    ```scss
    $yellow: #fce473 
    .quote{ border-left: 5px solid $yellow;}    //.quote{ border-left: 5px solid #fce473;}
    ```
- to see the variable power in effect
    ```scss
    $pink: #ff1493;
    .quote{ border-left: 5px solid $pink;}
    .button{ background: $pink;}
    .sidebar a:hover{ border-bottom-color: $pink;}
    .footer a{ color: $pink;}
    ```
- if you need to change to a different shade of pink, just have to change the color value **once**
    ```scss
    $pink: #c71585;
    ```
- another example: variable in variable
    ```scss
    // Defining color values
    $yellow: #fce473;
    $pink: #c71585;
    $green: #32cd32;
    $blue: #1d90ff;

    // Defining color types
    $primary-color: $green;

    .quote{ border-left: 5px solid $primary-color;}
    .button{ background: $primary-color;}
    .sidebar a:hover{ border-bottom-color: $primary-color;}
    .footer a{ color: $primary-color;}
    ```
- if you do decide to use `$blue` instead of `$green`, you'd only have to modify one line
- setting other type of content
    ```scss
    // Colors
    $yellow:              #fce473;
    $pink:                #c71585;
    $green:               #32cd32;
    $blue:                #1d90ff;

    $primary-color:       $blue;
    $secondary-color:     $yellow;

    // Fonts
    $serif:               "Lora", "Playfair Display", Georgia, serif;
    $sans-serif:          "Roboto", "Source Sans Pro", "Open Sans", Arial, sans-serif;
    $monospace:           "Inconsolata", monospace;

    $primary-font:        $sans-serif;
    $secondary-font:      $serif;

    // Spacing
    $mobile-space:        10px;
    $desktop-space:       35px;
    ```

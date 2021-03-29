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

> ### [NESTING: prevents repeating selectors](https://marksheet.io/sass-nesting.html)
- nesting CSS rules within parent/child selectors allow to define hierarchy selectors
    ```scss
    .parent{
        .child{}        //using hierarchy translates into a space in CSS
    }
    .title{
        color: $yellow;
        strong{}
        em{}
    }
    ```
- will be compiled into CSS
    ```css
    .parent .child{}    <!-- a space btw .parent and .child defines hierarchy -->
    .title{ color: #fce473 }
    .title strong{} 
    .title em{} 
    ```
- nesting CSS rules with pseudo-selectors (altered state) like :hover using ampersand
- nesting CSS rules with joined classes using ampersand
    ```scss
    .parent{
        &:hover{}       //using & translate into no space in CSS
        &.another-class{}
    }
    ```
- will be compiled into CSS
    ```css
    .parent:hover{}           <!-- pseudo-selectors have no space before -->
    .parenet.another-class{}  <!-- HTML elements that have class="parent another-class" - no space -->
    ```
- more example from CSS to SCSS
    ```css
    <!-- this is CSS -->
    .description{}
    .description p{}
    .description p a{}
    .description p a:hover{}
    .description p strong{}
    .description table{}
    .description table tr{}
    .description table tr:nth-child(2n){}
    .description table th,
    .description table td{ color: #111111 }
    .description table td.empty,
    .description table th.empty{ font: "xxxxx" }
    .description table th{}
    ```
    ```scss
    //this is SCSS
    .description{
        p{
            a{
                &:hover{}
            }
            strong{}
        }
        table{
            tr{
                &:nth-child(2n){}
            }
            th,
            td{
                color: #111111
                &.empty{ font: "xxxxx" }
            }
            th{}
        }
    }
    ```

> ### [MIXINS and EXTENSIONS: prevents repeating properties](https://marksheet.io/sass-mixins.html)
- mixins:
    - avoid writing the same CSS code over and over again
    - custom CSS functions that can accept parameters
    - can `include` to reuse function code whenever/wherever you want
        ```scss
        @mixin overlay(){   //overlay is name of mixin
            bottom: 0;
            left: 0;
            position: absolute;
            right: 0;
            top: 0;
        }
        .modal-background{
            @include overlay();     //reference overlay mixin using @include
            background: black;
            opacity: 0.9;
        }
        ```
    - this .scss will be compiled into .css:
        ```css
        .modal-background{
            bottom: 0;
            left: 0;
            position: absolute;
            right: 0;
            top: 0;
            background: black;
            opacity: 0.9;
        }
        ```
    - reusing mixin
        ```scss
        .modal-background{
            @include overlay();
        }
        .product-link{
            @include overlay();
        }
        .image-pattern{
            @include overlay();
        }
        ```
    - to alter the output, mixins can accept parameters
        ```scss
        @mixin border-radius($radius) {
            -webkit-border-radius: $radius;
            -moz-border-radius: $radius;
            -ms-border-radius: $radius;
                border-radius: $radius;
        }

        .box{
            @include border-radius(3px);
        }
        ```
    - can also include optional parameters with default value
        ```scss
        @mixin label($text: "Code", $background: $yellow, $color: rgba(black, 0.5)) {
            position: relative;
            &:before{
                background: $background;
                color: $color;
                content: $text;
                display: inline-block;
                font-size: 0.6rem;
                font-weight: 700;
                height: 1rem;
                left: 0;
                letter-spacing: 0.1em;
                line-height: 1rem;
                padding: 0 0.5em;
                position: absolute;
                text-transform: uppercase;
                top: 0;
            }
        }

        div.highlighter-rouge{
            @include label();       //div.highlighter-rouge will use the mixin's default values
            &.css{
                @include label("CSS", $blue, white);    //.css will use different labels and colors
            }
            &.scss{
                @include label("SCSS", #c69, white);    //.scss will use different labels and colors
            }
        }
        ```
    - other mixin libraries:  
        [Bourbon](https://bourbon.io)  
        [Compass](https://compass-style.org)  
        [Susy](https://susy.oddbird.net)  



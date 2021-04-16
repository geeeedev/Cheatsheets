## Purpose: Remind myself some basics of SCSS

1. Two CSS preprocessors to choose from:
    - [Less](https://lesscss.org/) - JavaScript
    - [Sass](https://sass-lang.com/) - Ruby On Rail

1. Sass has two syntaxes avail:
    - Sass (Syntactically Awesome SytleSheets) in .sass files - indentations
    - SCSS (Sassy CSS) in .scss files - syntax more closely to CSS

1. Remember:
    - Sass is the name of the preprocessor
    - SCSS is more similar to CSS and easier to adopt/remember
    - all resources online mention Sass, not SCSS
    - all features are available for both syntax
    - everything in SCSS is available in Sass
    - a CSS file is a valid SCSS file - compatibility  
    - difference between Sass and SCSS is [subtle](https://sass-lang.com/documentation/syntax).
&nbsp;  
&nbsp;  

> ### INSTALLATION
- [follow installation here](https://sass-lang.com/install)
- install on Mac OSX using Homebrew (the Dart Sass - Standalone/DartVM version - fastest/latest/greatest/Recommended)
- Note the path to the Dart SDK: /usr/local/opt/dart/libexec
    ```
    brew install sass/sass/sass
    ```
    - instailling Dart Sass on the command line will enable running the sass executable to compile .sass and .scss files to .css files. (Recommended!)
        ```bash
        sass source/stylesheets/index.scss build/stylesheets/index.css
        sass SCSS/styles.scss CSS/styles.css   —- watch
        ```
        > watch means SASS is watching for changes to update the CSS files after each change  
        Once compile is done, .css files are available for importing into project as usual  
        A .css.map file will also be generated as part of the compilation  
    - Can run simultaneously with react project in development.  Just `npm start` on one terminal, and `sass <source.scss> <target.css> --watch` on another terminal.  Could even do a third terminal with `sass ... --watch` for modularizig .scss files.
&nbsp;  

- install using Node.js npm (pure JS implementation of Dart Sass - super slow! - NOT recommanded)
    ```
    npm install -g sass
    ```
    > NOTE asof April 2021:
    >- Node-Sass is another which integrates with react/webpack but Node-Sass is deprecated (obsolete) and should be avoided in new project.  
        1. `npm install node-sass@4.12.0` - version corresponds to existing Node version  
        2. import .scss files into component .js files as needed  
        3. `npm start` will automatically compile scss to css first  
        4. `npm uninstall node-sass` to uninstall if needed
    >- While sass (Dart JS version - NOT recommended as mentioned above) can work with React-scripts, it uses sass-loader v8 which prefers node-sass over sass (Dart JS version) - also NOT recommended
    >- Best to stick with Dart Sass Standalone version and run Dart compiler `sass` separately for best performance for now!  

&nbsp;  
> also read resources [adding to your PATH](https://katiek2.github.io/path-doc/)  
> Note the path to the Dart SDK: /usr/local/opt/dart/libexec

&nbsp;  

## SCSS Features:
### Everything about Sass/SCSS is to provide tools for **DRY**
> [See more specifics in SASS/SCSS documentation](https://sass-lang.com/documentation/style-rules)  
> [Also see flow control in SCSS](https://sass-lang.com/documentation/at-rules/control)
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



> ### [MIXINS / EXTENSIONS / PLACEHOLDERS: prevents repeating properties](https://marksheet.io/sass-mixins.html)
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



- extensions: 
    - avoid writing the same set of properties across diff CSS rules
    - to inherit the same CSS properties of another selector
        ```scss
        .small-uppercase{
            color: lightslategrey;
            font-size: 10px;
            letter-spacing: 0.1em;
            line-height: 12px;
            text-transform: uppercase;
        }
        .modal-background{
            @extend .small-uppercase;
        }
        .product-link{
            @extend .small-uppercase;
        }
        .image-pattern{
            @extend .small-uppercase;
        }
        ```
        ```css
        <!-- generated css -->
        .small-uppercase,       <!-- note that .small-uppercase is included in the common props list -->
        .modal-background,
        .product-link,
        .image-pattern{
            color: lightslategrey;
            font-size: 10px;
            letter-spacing: 0.1em;
            line-height: 12px;
            text-transform: uppercase;
        }
        ```
    - @extend regroups common properites under a list of selectors
    - @extend is more efficient than @mixin/@include, as it only writes the common properties **once**
        ```scss
        // scss
        @mixin small-uppercase() {
            color: lightslategrey;
            font-size: 10px;
            letter-spacing: 0.1em;
            line-height: 12px;
            text-transform: uppercase;
        }

        .modal-background{
            @include small-uppercase();
        }

        .product-link{
            @include small-uppercase();
        }

        .image-pattern{
            @include small-uppercase();
        }

        // generated css
        .modal-background{
            color: lightslategrey;
            font-size: 10px;
            letter-spacing: 0.1em;
            line-height: 12px;
            text-transform: uppercase;
        }

        .product-link{
            color: lightslategrey;
            font-size: 10px;
            letter-spacing: 0.1em;
            line-height: 12px;
            text-transform: uppercase;
        }

        .image-pattern{
            color: lightslategrey;
            font-size: 10px;
            letter-spacing: 0.1em;
            line-height: 12px;
            text-transform: uppercase;
        }
        ```

- placeholders:
    - in the case the `.small-uppercase` **selector** is not needed, transform it into a **Sass placeholder** 
    - replace the dot with a percentage sign `%`
        ```scss
        %small-uppercase{
            color: lightslategrey;
            font-size: 10px;
            letter-spacing: 0.1em;
            line-height: 12px;
            text-transform: uppercase;
        }

        .modal-background{
            @extend %small-uppercase;
        }

        .product-link{
            @extend %small-uppercase;
        }

        .image-pattern{
            @extend %small-uppercase;
        }
        ```
        ```css
        <!-- generated css -->      <!-- note that .small-uppercase is NOT included in the common props list, unlike extensions -->
        .modal-background,
        .product-link,
        .image-pattern{
            color: lightslategrey;
            font-size: 10px;
            letter-spacing: 0.1em;
            line-height: 12px;
            text-transform: uppercase;
        }
        ```
    - the `%small-uppercase` rule is only here to provide a location for common properties

- Difference between mixins, extensions, and placeholders:  
    > @extend and %placeholder are more elegant and efficient, while mixins are more straightforward

    |        | Definition | Referencing | Combines Selectors? | Allow Params? | Can be used on its own? |
    | ------ |------      |------       |------               |------         |------                   |
    | **Mixins** | @mixin name() | @include name() | No | `Yes` | No |
    | **Extensions** | any class | @extend .class | `Yes` | No | `Yes` |
    | **Placeholders** | %placeholderName | @extend %placeholderName | `Yes` | No | No |  
&nbsp;  
&nbsp;  


> ### OPERATORS: 
- add/subtract/multiply/divide
- `960px / 4`  or  `$space * 2`  
&nbsp;  


> [See more specifics in SASS/SCSS documentation](https://sass-lang.com/documentation/style-rules)
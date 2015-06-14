Bootswatch SASS
==========

Bootswatch is a collection of free themes for [Bootstrap](http://getbootstrap.com/). Check it out at [bootswatch.com](http://bootswatch.com).

This fork is a port to SASS so you can include swatches in your Bootstrap SASS project.

Usage
-----
####CSS
Download the `bootstrap.min.css` file associated with a theme and replace Bootstrap's default stylesheet.

The themes are also hosted on [BootstrapCDN](http://www.bootstrapcdn.com/).

####SCSS / Bower
Add it to your bower_components directory by executing

    bower install bootswatch-sass

To use a theme in your Sass project, structure your imports in this order

1. import the offial bootstrap-sass variables
2. import bootswatch theme variables
3. import offical bootstrap-sass
4. import bootswatch theme additional file

E.g - Importing the paper theme:
```css
    @import "bower_components/bootstrap-sass-official/assets/stylesheets/bootstrap/variables";
    @import "bower_components/bootswatch-sass/paper/variables";
    @import "bower_components/bootstrap-sass-official/assets/stylesheets/bootstrap/bootstrap";
    @import "bower_components/bootswatch-sass/paper/bootswatch-scss/readable/bootswatch";
```

Customization
------
Bootswatch is open source and you’re welcome to modify the themes.

Each theme consists of two SASS files. `_variables.scss`, which is included by default in Bootstrap, allows you to customize [these settings](http://getbootstrap.com/customize/#less-variables). `_bootswatch.scss` introduces more extensive structural changes.

Check out the [Help page](http://guru-digital.github.io/bootswatch-sass/help/) for more details on building your own theme.

API
-----

A simple API is available for integrating your platform with Bootswatch. Send your request to `http://guru-digital.github.io/bootswatch-sass/api/3.json`.

The swatch objects are returned in an array called `themes`, each one with the following properties:  `name`, `description`, `preview`, `thumbnail`, `css`, `cssMin`, `scss`, and `scssVariables`.

More info at http://guru-digital.github.io/bootswatch-sass/help/#api

Author
------

####Official Bootswatch

   Thomas Park

+ http://github.com/thomaspark
+ http://thomaspark.me

####Bootswatch-sass

   Corey Sewell

+ http://github.com/guru-digital
+ http://gdmedia.tv


Thanks
------
[Thomas Park](http://thomaspark.me) for [Bootswatch](http://bootswatch.com/).

[Mark Otto](http://github.com/markdotto) and [Jacob Thornton](http://github.com/fat) for [Bootstrap](https://github.com/twitter/bootstrap).

[Jenil Gogari](http://www.jgog.in/) for his contributions to the Flatly theme.

[James Taylor](http://github.com/jostylr) for [cors-lite](https://github.com/jostylr/cors-lite).


Copyright and License
----
Copyright 2014 Thomas Park

Code released under the MIT License.

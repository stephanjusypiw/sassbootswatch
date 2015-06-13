## Laravel PHP Framework

[![Build Status](https://travis-ci.org/laravel/framework.svg)](https://travis-ci.org/laravel/framework)
[![Total Downloads](https://poser.pugx.org/laravel/framework/downloads.svg)](https://packagist.org/packages/laravel/framework)
[![Latest Stable Version](https://poser.pugx.org/laravel/framework/v/stable.svg)](https://packagist.org/packages/laravel/framework)
[![Latest Unstable Version](https://poser.pugx.org/laravel/framework/v/unstable.svg)](https://packagist.org/packages/laravel/framework)
[![License](https://poser.pugx.org/laravel/framework/license.svg)](https://packagist.org/packages/laravel/framework)

### License

The Laravel framework is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)

### Tutorial on how to use Laravel 5 and Elixir SASS with Bootswatch

Note:  I am assuming that you have installed **node**, **gulp** and 
       **bower** on your development machine.

1. In the root directory of your Laravel 5 application type the following at the command prompt: 
	```
	npm install
    ```
	Note : The command **npm install** 
    is used in order to install **gulp** and **laravel-elixir** locally.

	If you get an error message in OSX try typing the following at the command prompt:
	```
	sudo npm install
    ```
   (Note:  type **npm -v** to find the current version of current version of node)
 
2.  If you look at your Laravel 5.1 directory structure, you will now see a new folder under
 	the root folder called **node_modules**.  Will see a hidden **.bin**, **gulp** and **laravel-elixir**
 	folder.

3.  Check to see if gulp is installed in the root folder of your application
    by typing the following at the command prompt: 
    
    ```
	gulp -v
	```
	
    In my case the output is:
	```
	-> gulp -v
	[07:45:14] CLI version 3.9.0
	[07:45:14] Local version 3.9.0
	```
	
4.  If gulp is not installed type the following at the command prompt:
	```	
	npm install --global gulp
	or
	sudo install --global gulp
	```
	
5. Now there are a couple of ways to install **bootstrap-sass**. I’ve decided to use bower since 
   it’s fairly easy.
   To see if bower is installed type the following at the command prompt:
   ```
   	bower -v
   ```
   If bower is not installed on your system, type the following at the command prompt:
   ```
   npm install -g bower
   ```
   
6. In the root folder of your application initialise bower with the following at the command prompt:
   ```
   bower init
   ```
   Answer the questions the best you can.  
   A new **bower.json** will be created in root folder of your application.  
   You can edit the **bower.json** file later if you wish.

7. Create a **.bowerrc** at the root of your project and put the following code in the **.bowerc** file:
	```
	{
		"directory": "vendor/bower_components"
	}
	```
    With that code, we specify where all our libraries will be stored.  In this 
    case **vendor/bower_components**.

8.  Let's now install bootstrap-sass. In the root folder of your application type the 
    following at the command prompt to search for bootstrap-sass:
    ```
	bower search bootstrap-sass
	```
	You will see the list of bootstrap-sass options.

    **************
    
9.  In the root of your application type the following at the command prompt to retrieve
    bootstrap-sass:
    ```
	bower install bootstrap-sass-official --save
    ```
	This will install bootstrap-sass-official. 
	Now look in the **vendor/bower_components** folder.  There should be
    2 new folders called **bootstrap-sass-official** and **jquery**.  This means we
    don't need to look for the jquery library since it comes with **bootstrap-sass-official**.
	
	
	**************
	
10.  Next I installed bootstrap.  I only installed bootstrap for the jQuery dependency.
     In the root of your application type the following at the command prompt:
    ```
    bower install bootstrap-bootstrap --save
    ```
    
    This will install bootstrap with jQuery. 

	Now look in the **vendor/bower_components** folder.  There should be
	3 new folders called **bootstrap-sass-official**, **bootstrap** and **jquery**.
	
11. 

10. In the root of your application type the following at the command prompt:
    ```
	bower search bootswatch
    ```
	To see a list of bootswatch options.


11. In the root of your application type the following at the command prompt:
	```	
	bower install bootswatch --save
    ```

12.  Now look in the **vendor/bower_components** folder.  There should be
	 a new folder called **bootswatch**.

13. View the **bower.json** file to see the new dependencies that have been added.


14. By default Laravel 5 uses less, so the file **gulpfile.js** should look like
    the code below:
    ```
    elixir(function(mix) {
    	mix.less('app.less');
    });
    ```
    
15. Now delete the folder **resources/less/boostrap** (that comes with the default installation of Laravel 5)
 	 We will not use this folder.

16. Delete the contents of the file **resources/less/app.less**.  This file should now
 	 be empty.

17. Add a simple CSS class to the file **resources/assets/less/app.less**. 
    In this case a CSS class called **.flash**.  You can thank Jeffrey Way for this class.
    ```
    .flash {
        background: #f66422;
    } 
    ```

18. In the **public** folder delete the folder **css** (this folder has a **app.css** file that you will
    also delete)


19. Now let's compile the new **app.less** file into a css file.  In the root directory of the Laravel 5
 	application type the following at the command prompt:
    ```
 	gulp
    ```
    
20.  Your **public** folder should now contain the complied **app.css** file inside
     a folder called css.  Yippee....... this worked!

21.  The next step is to expand the **gulpfile.js** to include Bootstrap, Bootswatch and
     jQuery.  This is the new **gulpfile.js** file.
     Note:  Many thanks to **raygun** from Laracasts who created the original **gulpfile.js** file.
            I could not get the correct result WITHOUT raygun's **gulpfile.js** file.

    ```
    var elixir = require('laravel-elixir');
    
    elixir(function(mix){
        // Copy the files that bower has fetched. Note that gulp tasks run
        // asynchronously. 
        mix.copy(
            'vendor/bower_components/jquery/dist/jquery.js',
            'resources/assets/js/jquery.js'
            // I will use the cerulean bootswatch theme
        ).copy(
            'vendor/bower_components/bootswatch/cerulean',
            'resources/assets/less/cerulean'
        ).copy(
            'vendor/bower_components/bootstrap/less',
            'resources/assets/less/bootstrap'
        ).copy(
            'vendor/bower_components/bootstrap/dist/js/bootstrap.js',
            'resources/assets/js/bootstrap.js'
        ).copy(
            'vendor/bower_components/bootstrap/dist/fonts',
            'public/fonts'
        );

        // Combine scripts
        mix.scripts([
                'js/jquery.js',
                'js/bootstrap.js'
            ],
            'public/js/admin.js',
            'resources/assets'
        );

        // Compile Less into the public/css folder
        mix.less('app.less', 'public/css');
    });
    
	```

22.  In the **resources/assests/app.less** file add the imports
	```
	@import "bootstrap/bootstrap";
	@import "cerulean/variables";
	```

23. Finally, if you want the entire bootswatch themes then change your **gulpfile.js**
   as show shown below:


   Old Code:
   ```
        // I will use the cerulean bootswatch theme
		    ).copy(
		        'vendor/bower_components/bootswatch/cerulean',
		        'resources/assets/less/cerulean'
   ```
    New Code:
    ```
    	     // I will use the entire bootswatch library
    		).copy(
        		'vendor/bower_components/bootswatch',
        		'resources/assets/less/bootswatch'
    ```
     Then in your ***resources/assests/app.less*** file add the following if you
     want, say the cosmo theme.
     ```
     @import "bootstrap/bootstrap";
     @import "bootswatch/cosmo/variables";
     ```
     **NOTE:  DON'T FORGET TO RUN gulp AT THE COMMAND LINE AFTER YOU EDIT THE
     resources/assests/app.less file!**
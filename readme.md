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
   
   **************
 
2.  If you look at your Laravel 5.1 directory structure, you will now see a new folder under
 	the root folder called **node_modules**.  You will see a hidden **.bin**, **gulp** and **laravel-elixir**
 	folders.
 	
 	**************

3.  Check to see if **gulp** is installed in the root folder of your application
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
	
	**************
	
4.  If **gulp** is not installed type the following at the command prompt:
	```	
	npm install --global gulp
	or
	sudo install --global gulp
	```
	
	**************
	
5. Now there are a couple of ways to install **bootstrap-sass**. I’ve decided to use **bower** since 
   it’s fairly easy.
   To see if **bower** is installed type the following at the command prompt:
   ```
   	bower -v
   ```
   If **bower** is not installed on your system, type the following at the command prompt:
   ```
   npm install -g bower
   ```
   
   **************
   
6. In the root folder of your application initialise bower with the following at the command prompt:
   ```
   bower init
   ```
   Answer the questions the best you can.  
   A new **bower.json** will be created in root folder of your application.  
   You can edit the **bower.json** file later if you wish.
   
   **************

7. Create a **.bowerrc** at the root of your project and put the following code in the **.bowerc** file:
	```
	{
		"directory": "vendor/bower_components"
	}
	```
    With that code, we specify where all our libraries will be stored.  In this 
    case **vendor/bower_components**.
    
    **************
    
8.  Let's now install **bootstrap-sass-official**. In the root folder of your application type the 
    following at the command prompt to search for **bootstrap-sass**:
    ```
	bower search bootstrap-sass
	```
	You will see the list of bootstrap-sass options.

    **************
    
9.  In the root of your application type the following at the command prompt to retrieve
    **bootstrap-sass**:
    ```
	bower install bootstrap-sass-official --save
    ```
	This will install bootstrap-sass-official. 
	Now look in the **vendor/bower_components** folder.  There should be
    2 new folders called **bootstrap-sass-official** and **jquery**.  This means we
    don't need to look for the jquery library since it comes with **bootstrap-sass-official**.
	
	
	**************
	
10.  Let's now install **bootswatch-sass**. In the root of your application type the following 
     at the command prompt to see a list of **bootswatch-sass** options.
    ```
	bower search bootswatch-sass
    ```
	
    **************
    
11. Install **bootswatch-sass** in the root of your application. 
    Type the following at the command prompt:
	```	
	bower install bootswatch-sass --save
    ```

    If you are prompted, select the latest version of **bootstrap-sass-official**
    
    **************
    
12.  Now look in the **vendor/bower_components** folder.  There should be
	 a new folder called **bootswatch-sass**.  Notice that you have all the
	 bootswatch themes under the **bootswatch-sass** folder.
	 
	 **************
	 
13. View the **bower.json** file to see the new dependencies that have been added.

    **************
    
14. By default Laravel 5.1 uses less, so the file **gulpfile.js** should look like
    the code below:
    ```
    elixir(function(mix) {
    	mix.less('app.less');
    });
    ```
    
    **************
    
15. Rename the code in the **gulpfile.js** as shown below:
    ```
    elixir(function(mix) {
        mix.sass('app.scss');
    });
    ```
    
    
16. Rename the folder **resources/assets/less** (that comes with the default installation of Laravel 5.1)
    to **resources/assets/sass**.
    
    **************
    
17. Rename the file **resources/assets/sass/app.less** (that comes with the default installation of Laravel 5.1)
    to **resources/assets/sass/app.scss**.

    **************
    
18. Delete the contents of the file **resources/assets/sass/app.scss**.  This file should now
 	be empty.

    **************
    
19. Add a simple CSS class to the file **resources/assets/sass/app.scss**. 
    In this case a CSS class called **.flash**.  You can thank Jeffrey Way for this class.
    ```
    .flash {
        background: #f66422;
    } 
    ```
    
    **************


20. Look In the **public** folder. Currently there is NO folder called **css**.  When we compile
    the **app.scss** file into a **app.css** file, a new folder called **public/css** will be created.

    **************


21. Now let's compile the new **app.scss** file into a **css** file.  In the root directory of the 
    Laravel 5.1 application type the following at the command prompt:  
    ```
 	gulp
    ```
    
    **************
     
22.  Your **public** folder should now contain the complied **app.css** file inside
     a folder called **css**.  Yippee....... this worked!

    **************
    
    
23.  I am assuming that you have created a HomeStead Virtual Machine and
     configured the necessary files so that you can view your application's home using
     directory using a browser.

     Let's replace the default **welcome.blade.php** file with the code below to see
     **bootstrap** and **bootswatch** working.  (It won't work at this stage, but we will get
     there soon).  Notice the call to the CSS file called **css/app.css** and the 
     Javascript file called **js/app.js**
    
    ```
 
       <html>
       <head>
           <title>Laravel</title>
           <link href='//fonts.googleapis.com/css?family=Lato:100' rel='stylesheet' type='text/css'>
           <link href="css/app.css" rel="stylesheet" type="text/css">
       </head>
       <body>
       <nav class="navbar navbar-default">
           <div class="container-fluid">
               <!-- Brand and toggle get grouped for better mobile display -->
               <div class="navbar-header">
                   <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bs-example-navbar-collapse-1">
                       <span class="sr-only">Toggle navigation</span>
                       <span class="icon-bar"></span>
                       <span class="icon-bar"></span>
                       <span class="icon-bar"></span>
                   </button>
                   <a class="navbar-brand" href="#">SASS with Bootswatch - 2015</a>
               </div>
               <!-- Collect the nav links, forms, and other content for toggling -->
               <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
                   <ul class="nav navbar-nav">
                       <li><a href="#">stephanj - 2015</a></li>
                       <li class="dropdown">
                           <a href="#" class="dropdown-toggle" data-toggle="dropdown" role="button" aria-expanded="false">Dropdown <span class="caret"></span></a>
                           <ul class="dropdown-menu" role="menu">
                               <li><a href="#">Action</a></li>
                               <li><a href="#">Another action</a></li>
                               <li><a href="#">Something else here</a></li>
                               <li class="divider"></li>
                               <li><a href="#">Separated link</a></li>
                           </ul>
                       </li>
                   </ul>
               </div><!-- /.navbar-collapse -->
           </div><!-- /.container-fluid -->
       </nav>
       <script src="js/app.js"></script>
       </body>
       </html>
   
	```
	
     **************
    
24.  The next step is to expand the **gulpfile.js** to include **bootstrap**, **Bootswatch** and
     **jQuery**.  This is the new **gulpfile.js** file. 
  
     ```
     
     var elixir = require('laravel-elixir');
     
     
     // create variables for paths for bootstrap and bootswatch
     var bowerDirBootstrap = "vendor/bower_components/bootstrap-sass-official/assets/";
     var bowerDirBootswatch = "vendor/bower_components/bootswatch-sass";
     // javascript paths
     var bowerDirJquery = "vendor/bower_components/jquery/dist/";
     
     elixir(function(mix) {
         mix.sass('app.scss')
             // copy relevant files to the resources folder.  This is the css
             .copy(bowerDirBootstrap, 'resources/assets/sass/bootstrap')
             .copy(bowerDirBootswatch, 'resources/assets/sass/bootswatch')
             // this is the javascript
             .copy(bowerDirJquery + 'jquery.js', 'resources/assets/js/jquery.js')
             .copy(bowerDirBootstrap + 'javascripts/bootstrap.js',
             'resources/assets/js/bootstrap.js')
         //
         // Combine scripts
         //
         mix.scripts([
                 'js/jquery.js',
                 'js/bootstrap.js'
             ],
             'public/js/app.js',
             'resources/assets'
         );
     
     });
     
     ```
     
     **************
     
25.  Compile the new **app.scss** file into a **css** file.  In the root directory of the 
     Laravel 5.1 application type the following at the command prompt:  
     ```
      	gulp
     ```
         
     Notice the 2 new folders in ***resources/assets/sass** folder called **bootstrap** 
     and **bootswatch**.
     
     **************
     
26.  In the **resources/assests/app.scss** file add the imports for **bootstrap** and
     **bootswatch**.
	
	```
	// first import bootstrap variable
    @import "bootstrap/stylesheets/bootstrap/variables";
    // second import the COSMO theme variables
    @import "bootswatch/cosmo/variables";
    // third import bootstrap
    @import "bootstrap/stylesheets/bootstrap";
    // forth import cosmo bootswatch
    @import "bootswatch/cosmo/bootswatch";
    
    .flash {
      background: #f66422;
    }

	```

    **************


27. In the root directory of the Laravel 5.1 application type the following 
    at the command prompt: 
     ```
     gulp
     ```

28.  Refresh the home page of your application to see the bootswatch COSMO theme
     being used on the Navigation Bar.
     
     **************
     
     **NOTE:  DON'T FORGET TO RUN gulp AT THE COMMAND LINE AFTER YOU EDIT THE
     resources/assests/app.scss file!**
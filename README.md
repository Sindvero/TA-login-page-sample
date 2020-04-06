# Login page with Google OAuth

## Installation

The best way to create a login with OAuth and Laravel framework is to create the project from scratch (this repo is here to help with some files, you will have the same project by creating it by yourself).

First of all, you need to install several things into the server:

* php and mysql: ```sudo apt-get install php7.2  php7.2-mysql mysql-server``` 
* composer: ```curl -sS https://getcomposer.org/installer -o composer-setup.php``` <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;            ```sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer```
* check the installation with: ```composer```
* Mbstring PHP Extension: ```sudo apt-get install php7.2-mbstring```
* XML PHP Extension: ```sudo apt-get install php7.2-xml```

After having installed all the above depedencies, you need to create you project and run:
```
composer create-project --prefer-dist laravel/laravel myProject
```

Then you need to run ```composer install``` to import your packages.

Then, you need to configure the **.env** file by adding you database information.

Now you should be able to run:
* ```php artisan migrate```
* ```php artisan serve```

and go to http://localhost:8000/login to see your login page.

## Configure OAuth

In order to add Google OAuth, you need to install socialite Package: ```composer require laravel/socialite```

You will need to add 2 lines to the ./config/app.php:

* Laravel\Socialite\SocialiteServiceProvider::class,    In provider;
* Socialite' => Laravel\Socialite\Facades\Socialite::class, in aliases.

You need to create a controller for Google OAuth: ```php artisan make:controller GoogleAuthController```
Then:
* Go to ./app/Http/Controllers/GoogleAuthController.php and paste my code to your project;
* Go to ./routes/web.php and paste my code.

Now you need to create a  Goolge Client ID:

* Go to https://console.developers.google.com/apis/dashboard and login with your hawk account;
* Create a new project
* OAuth consent screen -> check Internal to only authorize connection from a hawk account -> create -> give a name to your application and save
* Credentials -> Create Credentials -> Create OAuth client ID -> Check Web application -> give it a name -> in Authorized redirect URIs give 'http://localhost:8000/login' and Create.
* You will have a pop-up with your client ID and client secret.

Go back to you project and in ./config/services.php add:
```
'google' => [
         'client_id' => 'YourClientID',
         'client_secret' => 'YourClientSecret',
         'redirect' => 'http://localhost:8000/callback'
    ],

```

Go to ./ressources/views/auth/login.blade.php and a button to connect with Google (see mine)

Run ```php artisan serve``` and go to http://localhost:8000/login

You should be able to connect with your account account.
Laravel Shibboleth Service Provider
===================================

Shibboleth Authentication for Laravel

Include the follwoing in your composer.json file and run composer update or install if it's a new project.

<pre><code>{
    "require": {
        "saitswebuwm/shibboleth": "dev-master"
    }
}</code></pre>

Include the following line to the end of your /app/config/app.php  'providers array'

<pre><code>'Saitswebuwm\Shibboleth\ShibbolethServiceProvider'</code></pre>

You will also need to change your auth driver in /app/config/auth.php

<pre><code>'driver' => 'shibboleth'
'model' => 'Saitswebuwm\Shibboleth\UserShibboleth'</code></pre>

Alternatively instead of setting model it is recommended you add the following to your User Model.

<pre><code>protected $fillable = array('email', 'first_name', 'last_name', 'password', 'type');</code></pre>

Add the included .htaccess file to your public folder. This should work for everyone. If users must authenticate with shibboleth you will have to modify this as it's set up to allow for both shibboleth and non-shibboleth users by default.

Now we can set it up for your install. Run the following two commands to created the needed database tables and config file.

<pre><code>php artisan config:publish saitswebuwm/shibboleth
php artisan migrate --package="saitswebuwm/shibboleth"</code></pre>

You will need to configure your .htaccess with whatever your setup involves. By default I have included a .htaccess in the src directory that will allow both shibboleth and non shibboleth users to view the application. Place it in your public folder if this behavior will work for your application.

In the Config/Package/Saitswebuwm/Shibboleth/Shibboleth.php file you will need to change the  following two lines to point to your servers idp.
<pre><code>'idp_login' => 'your.idp.login',
'idp_logout' => 'your.idp.logout',</code></pre>

For more info on the setup see the wiki section of this repository.

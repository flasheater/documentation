## I don't want to install wallabag
If you can't or don't want to install Wallabag on your server, we suggest you create a free account on Framabag wich uses our software: read the complete documentation here (TODO write Create a framabag account).

## I want to install wallabag
 
[Download the latest wallabag version](http://www.wallabag.org/download) and unpack it. Copy the files on your web server.

## I want the latest copy
Check out [wallabag](https://github.com/wallabag/wallabag.git) by typing in your terminal:

    $ cd /path/to/your/webservers/public/dir
    $ git clone https://github.com/wallabag/wallabag.git
    $ cd wallabag

This will download the latest wallabag sources into the folder 'wallabag'.

## I want a docker image
TODO(flasheater): Explain docker install and config.

## Prerequisites for your web server
* [PHP 5.3.3 or more](http://php.net/manual/en/install.php)
* [SQLite](http://php.net/manual/en/book.sqlite.php) or [MySQL](http://php.net/manual/fr/book.mysql.php) or [PostgreSQL](http://php.net/manual/en/book.pgsql.php)
* [XML for PHP](http://php.net/xml)
* [PCRE](http://php.net/pcre)
* [Data filtering](http://php.net/manual/book.filter.php)
* [Tidy for PHP](http://php.net/tidy)
* [cURL](http://php.net/curl)
* [allow_url_fopen](http://www.php.net/manual/en/filesystem.configuration.php#ini.allow-url-fopen)
* [gettext](http://php.net/manual/en/book.gettext.php)

To ensure that your server has all the prerequisites, you can run the file `wallabag_compatibility_test.php` that is located in the `install` directory of wallabag.

## Installation of the dependencies 
In order to work properly, wallabag needs some dependencies. To install them, you have to use `composer`. In your wallabag folder, run the following commands:

    curl -s http://getcomposer.org/installer | php
    php composer.phar install

If you can't install `composer` (In order to work properly, Wallabag needs some dependencies), we provide you a [vendor.zip](http://wllbg.org/vendor) file to unpack in your wallabag directory. 

## Setup you webserver
TODO(flasheater): how to tell apache2 about wallabag

TODO(flasheater): how to tell nginx about wallabag

## Setup SSL
TODO(flasheater): How to secure wallabag.

## Permissions
Your web server needs a writing access to the ''wallabag'' folder. Assuming your server is Debian/Ubuntu, you could set the permissions like that:

    # chown -R www-data .
    # chgrp -R www-data .

## Setup your database
If you are the only user of wallabag, skip this step. `sqlite` is the default database backend and it is more than suited for single user purposes.
If you however, plan on supporting multiple users, it is recommended to use `mysql` or `postgresql`. Install it on your server and prepare it for wallabag to use.
There are 3 steps you need to perform:
 
* Create a database
* Create a database user
* Grant that user the right to modifiy the database

### Setting up `mysql`
Login to mysql as root user:

    $ mysql -u root -p
Create a database, you can choose the name freely, keep in mind however, that you will need it later to tell `wallabag` about it:

    $ CREATE DATABASE 'wallabag';
Create a local mysql user and secure it with a long password. Remember the password as you will need to tell `wallabag` about it: 

    $ CREATE USER '*newuser*'@'localhost' IDENTIFIED BY '*password*';
Allow your new user to access the previously created database. Adjust the database name if you have chosen a different one. However, keep the ".*" after the name. Now your mysql user is allowed to control on datbase and one database only:

    $ GRANT ALL PRIVILEGES ON wallabag.* TO '*newuser*'@'localhost';
Refresh the mysql privileges so you can immediatly put your new user to work:

    $ FLUSH PRIVILEGES;

### Setting up `postgresql`
Login to `postgresql` as postgres user:

    $ sudo su - postgres
    $ psql

Create a new database:

    # CREATE DATABASE 'wallabag';

Create a new user:

    # CREATE USER 'newuser' WITH PASSWORD 'password';

Give your new user all the permissions for the database:

    # GRANT ALL PRIVILEGES ON DATABASE 'wallabag' TO 'newuser';

Quit postgres:

    # \q

## Installation of wallabag. At last.
Access to wallabag from your web browser. If your server is correctly configured, you reach the setup screen.  

Fill your database type (`sqlite`, `mysql` or `postgresql`) and finally the information for your user account.

wallabag is now installed. 

## Login 

From your web browser, you reach the login screen : fill your username and your password to connect to your account.

If you have previously configured a database you need to pass in the credentials you then chose. This is how you let `wallabag` know that it is allowed to use your database.

The credentials for the `wallabag` user account are freely choosable. Pick a strong (long) password and any user name you like. You will need those to login with your `wallabag` clients (browser, Chrome or Firefox extension, Android app ,...).

If you want multiple users, you will be able to create those later on in th `config` section of the `wallabag` web interface.

Enjoy!

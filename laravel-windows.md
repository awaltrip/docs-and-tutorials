# Run a Laravel project on Windows

This tutorial is meant to guide total newbies to PHP / Laravel to run an existing Laravel project on your local Windows machine, including database creation, encrypted key generation, and more.

### Install prerequisites

1. Download wamp: http://www.wampserver.com/en/. Do not place wamp inside of a folder that has spaces (such as "Program Files"). A good place to save it is directly in the C:\ drive.
2. Follow wamp's instructions to install and start a server.
3. Update your Windows Path environment variable to point to your php folder within your wamp folder tree.
    - In your Windows search bar, type "environment" and choose "Edit the system environment variables", then click the "Environment Variables" button.
    - Add this directory to the Path System variable: `C:\wamp64\bin\php\php5.6.38` (or whatever php version number you have)
4. Download composer https://getcomposer.org/download/

### Clone and run the project

1. Clone the Laravel project from Git and place it within your `C:\wamp64\www` folder.
2. Use wamp/phpMyAdmin to create a local database.
    - When wampserver is running, click the green icon in the icon tray in your taskbar. then click phpMyAdmin.
    - Login with username: root and empty password.
    - Click "User accounts" tab. select "Add user account". Use this information:
	    - User name: homestead
	    - Host name: localhost
	    - Password: secret
	    - Check "Create database with same name and grant all privileges"
	    - Global privileges: Check all
	    - SSL: Require none
3. Open a terminal and `cd` into your project root directory.
4. Run `copy .env.example .env`
5. Run `composer install`
6. Run `npm install` (optional / if needed)
7. Run `php artisan key:generate`
8. In the .env file, make sure these options are set to match the credentials of the database you have just created: `DB_HOST`, `DB_PORT`, `DB_DATABASE`, `DB_USERNAME` and `DB_PASSWORD`.
9. Run `php artisan migrate`
10. Run `php artisan db:seed`
    - PRO TIP: You can combine the 2 previous commands into one command: `php artisan migrate:fresh --seed`
11. Finally, to run the project, run `php artisan serve`

#### You can now access the project in a browser at localhost:8000

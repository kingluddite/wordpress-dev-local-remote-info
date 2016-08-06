# Local Development

1. Download [WordPress](https://wordpress.org/)
2. Extract Zip
3. Rename `wordpress` folder to `bhs`
4. Create `Sites` folder inside user directory
5. Move `bhs` into `Sites`
6. Open Mamp
    * change root to point to new `Sites` folder
    * change `Set Web & MySQL ports to 80 and 3306`

![Mamp screenshot of ports](https://i.imgur.com/t6dPeAw.png)

## Create Database
1. Click `Open Web Start Page`

![mamp start page](https://i.imgur.com/KLxuxYj.png)

2. Click it `Tools` > `phpMyAdmin`
3. Create new database
    * Make sure to name in lowercase
    * make sure to not have spaces
    * use an underscore instead of space

## Adding Setting via Browser
1. goto this URL: [http://localhost/bhs]
2. Go through 2 pages
    * page 1 - choose language
    * page 2 - provided database information
        - database name: bhs_wp
        - username: root
        - password: root
        - host: localhost
        - table prefix: keep as `wp_`
    * page 3 - create access to WP Admin
        - Name of Site (any string)
        - username: admin
        - password: password
        - email: your email
        - check to turn off SEO

Once three pages are complete, you can access WordPress via [http://localhost/bhs](http://localhost/bhs)

And to login you access [http://localhost/wp-admin](http://localhost/wp-admin)

##WordPress Remote 
1. Export the localhost database
    * phpMyAdmin
    * Make sure you are inside the database you are exporting
    * click Export
    * Then click custom
    * Select all to select all tables
    * Click go and save to downloads
2. login to bluehost
3. CPanel - MySQL Database
    * Create a new database following naming convention used in creating database locally.
    * Make sure to store all remote database info in a file that is saved in a secure place outside of your wordpress project
    * Create a user and a password for that user
    * Make sure to give the user all privileges on that database
4. Create a subdomain (or use a domain you purchased)
5. Point the subdmain to a folder inside `public_html` on bluehost
    * this folder is the remote root of your WordPress Project
    * you can goto [wordpress.org](http://wordpress.org), download wordpress copy, extract and **FTP** to the `public_html/bshwp` (if that's what you named it)
       - or you can enable **SSH**, (takes a day)
       - tell bluehost.com about your public **ssh** key (look online for documentaton on how to do this)
    * **wp-cli** - you can also look at how to install **wp-cli** locally (using my notes or online) and see if you can find out how to install on bluehost but searching online) This makes installing wordpress so much easier. The combination of using **SSH** and **WP-CLI** will save you countless hours as a WordPress Theme Developer
    * you can also just go through the browser install of wordpress using the same 3 pages you used when installing WordPress locally
        - just remember that the DB information needs to be used (hopefully you saved it in a safe locatation)
    * `wp-config.php` should have the DB connection info inside it
        - on your local wordpress install the db info should be simple and differernt from the remote wordpress install which should be complex and hard to hack
    * don't forget to also create the info needed for your WP Admin access (the third page of the wordpress install process)
        - put in your username (don't use admin for remote username)
        - and use a complex password for remote
        - assess login via `URL/wp-admin`
        - save this information in a safe spot because if you lose admin credentials you will be locked out of your site

## Find and Replace all
Open your local .sql file in Sublime Text and replace all occurences of http://localhost/bhs with http://bhs.your-domain.com (the subdomain your created earlier)

## Make backup copy of remote database
Using phpMyAdmin on bluehost.com follow similar procedure to local export of database

## Delete remote copy of database.
Using phpMyAdmin on bluehost.com 
Select database and drop it.
Use with caution

## Import Database
Using phpMyAdmin on bluehost.com click import tab and point to your saved updated sql file with remote subdomain (or your live domain) URL swapped out.

## Use Filezilla FTP program
* connect via FTP
* set up ftp on bluehost if necessary and connect via Filezilla
* Transfer all:
    + plugins you added
    + themes you added
    + uploads you added

## Finally
Browse to subdomain you created (or live domain) and your local wordpress should now be identical to your remote wordpress

Also don't forget to update your permalinks in the WP Admin panel
And make sure that you get rid of the easy username and password by tranferring the admin password user content to a new user with a more hackerproof username and password. The email you add is important as it is used if you ever get locked out.
Don't forget to turn on SEO when the site is live.

# PHP Gists
## Error Reporting
[PHP Error Reporting Gist](https://gist.github.com/jesseoverright/76d47b4ff46953933c8c)

    <?php
    ini_set('display_errors',1);
    error_reporting(E_ALL);

## Curl POST request

Makes a post request

    <?php
    $url = 'http://www.yourapi.com';
    $post_values = array(
        'sample1' => 'value',
        'sample2' => 3,
        'sample3' => array(1,2)
    );

    try {
        $ch = curl_init($url);
        curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
        curl_setopt($ch, CURLOPT_POST, true);
        // use http_build_query for x-www-form-urlencoded requests
        // or array only for form-data requests
        curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($post_values));
        $output = curl_exec($ch);
    } catch (Exception $e) {
        // error handling        
    }

    var_dump($output);
    ?>


## Ubunto LAMP Provisioning

### install apache, mysql, php

    $ apt-get update
    $ apt-get install -y apache2 mysql-server-5.5 php5-mysql php5 php5-mcrypt # optional: php5-xdebug git curl

    # enable mod rewrite
    $ a2enmod rewrite
    $ sed -i 's/DocumentRoot \/var\/www\/html/DocumentRoot \/var\/www\/html\n        <Directory "\/var\/www\/html">\n            AllowOverride All\n        <\/Directory>/' /etc/apache2/sites-available/default.conf

### PHPMyAdmin

    # set mysql root password
    $ echo "mysql-server-5.5 mysql-server/root_password password $MYSQL_ROOT_PASSWORD" | debconf-set-selections
    $ echo "mysql-server-5.5 mysql-server/root_password_again password $MYSQL_ROOT_PASSWORD" | debconf-set-selections

    # configure phpmyadmin
    $ echo "phpmyadmin phpmyadmin/dbconfig-install boolean true" | debconf-set-selections
    $ echo "phpmyadmin phpmyadmin/app-password-confirm password $MYSQL_ROOT_PASSWORD" | debconf-set-selections
    $ echo "phpmyadmin phpmyadmin/mysql/admin-pass password $MYSQL_ROOT_PASSWORD" | debconf-set-selections
    $ echo "phpmyadmin phpmyadmin/mysql/app-pass password $MYSQL_ROOT_PASSWORD" | debconf-set-selections
    $ echo "phpmyadmin phpmyadmin/reconfigure-webserver multiselect apache2" | debconf-set-selections
    
    $ export DEBIAN_FRONTEND=noninteractive
    $ apt-get install -y phpmyadmin 

### Install Wordpress

```
    rm -rf /var/www/html
    git clone https://github.com/WordPress/WordPress /var/www/html

    cd /var/www/html
    latestTag=$(git describe --tags `git rev-list --tags --max-count=1`)
    git checkout tags/$latestTag

    # create wp-config
    cp /var/www/html/wp-config-sample.php /var/www/html/wp-config.php

    sed -i "s/database_name_here/$DATABASE_NAME/" /var/www/html/wp-config.php
    sed -i "s/username_here/$DATABASE_USER/" /var/www/html/wp-config.php
    sed -i "s/password_here/$DATABASE_PASSWORD/" /var/www/html/wp-config.php

    # replace generic salt values
    curl -s https://api.wordpress.org/secret-key/1.1/salt >> /usr/local/src/wp.keys
    sed -i '/#@-/r /usr/local/src/wp.keys' /var/www/html/wp-config.php
    sed -i "/#@+/,/#@-/d" /var/www/html/wp-config.php

    # create htaccess with permalinks enabled
    echo "
    # BEGIN WordPress
    <IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /
    RewriteRule ^index\.php$ - [L]
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule . /index.php [L]
    </IfModule>

    # END WordPress
    " >> /var/www/html/.htaccess

    # change permissions of wordpress to vagrant user
    chown -R vagrant:vagrant /var/www/html

    # symlink uploads folder
    if [ -d /vagrant/wp-content ];
    then
        rm -rf /var/www/html/wp-content
        ln -fs /vagrant/wp-content /var/www/html/wp-content
    fi
```
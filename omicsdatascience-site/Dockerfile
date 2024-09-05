FROM php:8.2-apache

# Installs MySQL and ZIP extensions (needs zlib1g-dev and libzip-dev package)
RUN apt-get update && apt-get install -y zlib1g-dev libzip-dev nano && docker-php-ext-install zip mysqli

# Makes /var/www/html writable
RUN chmod -R 755 /var/www

# Copies the site inside Apache
COPY ./website /var/www/html

# Adds .htaccess, apache2.conf and site-available files 
COPY ./.htaccess /var/www/html/.htaccess
RUN chmod 777 /var/www/html/.htaccess
COPY ./000-default.conf /etc/apache2/sites-available/000-default.conf
COPY ./apache2.conf /etc/apache2/apache2.conf

# Enables mod_rewrite
RUN a2enmod rewrite

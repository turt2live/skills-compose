FROM php:8.2-fpm

# Dependencies
RUN apt-get update && apt-get install -y zlib1g-dev libzip-dev

# Email
RUN pear install Mail
RUN pear install pear/Net_SMTP

# Other extensions
RUN docker-php-ext-install mysqli pdo pdo_mysql zip bcmath calendar bz2 gettext exif ftp
RUN docker-php-ext-enable mysqli pdo pdo_mysql zip bcmath calendar bz2 gettext exif ftp

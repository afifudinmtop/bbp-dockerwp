FROM wordpress:php7.4

# Install XDebug via pecl (avoids Debian bullseye apt 404 on git)
RUN pecl install xdebug-3.1.6

# Copy xdebug.ini to /usr/local/etc/php/conf.d/
COPY files-to-copy/ /

# Since this Dockerfile extends the official Docker image `wordpress`,
# and since `wordpress`, in turn, extends the official Docker image `php`,
# the helper script docker-php-ext-enable (defined for image `php`)
# works here, and we can use it to enable xdebug:
RUN docker-php-ext-enable xdebug

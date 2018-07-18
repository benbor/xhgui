# See https://github.com/docker-library/php/blob/master/7.1/fpm/Dockerfile
FROM php:7.2-fpm

MAINTAINER Boris Benkovski <biankouski@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

## Type docker-php-ext-install to see available extensions
RUN pecl install mongodb \
    && docker-php-ext-enable mongodb

COPY        composer /usr/local/composer

 # Install packages
RUN         apt update && \
            apt install -y --no-install-recommends ca-certificates git wget htop telnet unzip && \
            # Clone xhgui and install 0.7.1, then remove useless files
            git clone https://github.com/perftools/xhgui /usr/local/src/xhgui && \
            cd /usr/local/src/xhgui && \

            # Keep Master
            git checkout tags/0.9.0 && \
            cp /usr/local/composer ./composer && \
            php ./composer install -o && \
            rm -Rf .git \
                   .scrutinizer.yml \
                   .travis.yml \
                   phpunit.xml \
                   README.md \
                   tests && \
            chown www-data:www-data /usr/local/src/xhgui/cache && \
            # Clean
            apt purge git unzip -y  && \
            apt autoremove -y && \
            apt autoclean && \
            apt clean && \
            rm -rf /var/lib/apt/lists/* /usr/share/man/* /usr/share/doc/* /var/cache/* /var/log/*



#ENTRYPOINT ["cp -r .v", "docker-php-entrypoint", ""]

# Installing XhGui
#WORKDIR     /usr/local/src/xhgui
#COPY        conf/xhgui.config.php /usr/local/src/xhgui/config/config.php
## Install composer
#RUN         apt update && \
#            apt install -y --no-install-recommends curl && \
#            curl https://github.com/composer/composer/releases/download/1.6.5/composer.phar -s -S -o composer.phar && \
#            chmod 0755 composer.phar && \
#            ./composer.phar selfupdate --stable && \
#            sed -i 's/composer\.phar update/composer.phar install --no-dev/g' install.php && \
#            php install.php && \
#            chown -R www-data:www-data /usr/local/src/xhgui && \
#            # Clean
#            rm -f composer.phar && \
#            apt purge curl -y  && \
#            apt autoremove -y && \
#            apt autoclean && \
#            apt clean && \
#            rm -rf /var/lib/apt/lists/* /usr/share/man/* /usr/share/doc/* /var/cache/* /var/log/*

#RUN apt-get update && apt-get install -y \
#    openssl \
#    git \
#    unzip
#
## Install Composer
#RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#RUN composer --version
#
## Set timezone
#RUN ln -snf /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && echo ${TIMEZONE} > /etc/timezone
#RUN printf '[PHP]\ndate.timezone = "%s"\n', ${TIMEZONE} > /usr/local/etc/php/conf.d/tzone.ini
#RUN "date"
#
## Type docker-php-ext-install to see available extensions
#RUN docker-php-ext-install pdo pdo_mysql
#
#
## install xdebug
#RUN pecl install xdebug
#RUN docker-php-ext-enable xdebug
#RUN echo "error_reporting = E_ALL" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "display_startup_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "display_errors = On" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#RUN echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini
#
#
#RUN echo 'alias sf="php app/console"' >> ~/.bashrc
#RUN echo 'alias sf3="php bin/console"' >> ~/.bashrc
#
#WORKDIR /var/www/symfony

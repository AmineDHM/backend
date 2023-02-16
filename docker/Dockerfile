FROM php:8.1-apache

RUN a2enmod rewrite

RUN apt update \
    && apt install -y zlib1g-dev g++ git curl libicu-dev zip libzip-dev zip \
    && docker-php-ext-install intl opcache pdo pdo_mysql \
    && pecl install apcu \
    && docker-php-ext-enable apcu \
    && docker-php-ext-configure zip \
    && docker-php-ext-install zip

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

RUN curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar && \
    mv ./phpcs.phar /usr/local/bin/phpcs && \
    chmod +x /usr/local/bin/phpcs

RUN curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcbf.phar && \
    mv ./phpcbf.phar /usr/local/bin/phpcbf && \
    chmod +x /usr/local/bin/phpcbf

COPY apache.conf /etc/apache2/sites-enabled/000-default.conf

COPY . /var/www/backend

WORKDIR /var/www/backend

EXPOSE 80

CMD ["apache2-foreground"]

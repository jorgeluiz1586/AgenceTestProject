FROM openswoole/swoole:22.0.0-php8.2

RUN apt update && apt upgrade -y && \
    apt install curl bash git zip wget unzip cmake libzip-dev libonig-dev libfreetype6-dev libjpeg62-turbo-dev libpng-dev libpq-dev libicu-dev -y

RUN docker-php-ext-configure gd --with-freetype --with-jpeg && \
    docker-php-ext-install -j$(nproc) gd intl zip mbstring curl calendar exif pcntl && \
    docker-php-ext-install pdo pdo_mysql pdo_pgsql

RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

RUN curl -sL https://deb.nodesource.com/setup_18.x | bash - && \
    apt install nodejs && \
    npm update -g npm && \
    npm install -g sass typescript

WORKDIR /var/www

COPY ./ /var/www



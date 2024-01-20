FROM php:8.3-fpm

# PHP Extension
RUN apt-get update

#RUN apt-get install -y openssl zip unzip git curl
#RUN apt-get install -y libzip-dev libonig-dev libicu-dev
RUN apt-get install -y \
    openssl \
    build-essential \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    locales \
    zip \
    jpegoptim optipng pngquant gifsicle \
    vim \
    unzip \
    git \
    curl \
    libzip-dev \
    apt-utils \
    libonig-dev \
    libicu-dev

RUN apt-get install -y autoconf pkg-config libssl-dev libxml2-dev && \
    ln -fs /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

RUN docker-php-ext-install bcmath mbstring intl opcache exif
RUN docker-php-ext-install pdo pdo_mysql mysqli gd
RUN docker-php-ext-install gettext intl -j$(nproc)

RUN echo 'date.timezone="America/Sao_Paulo"' >> /usr/local/etc/php/conf.d/date.ini
ENV TZ="America/Sao_Paulo"

# Redis
RUN mkdir -p /usr/src/php/ext/redis; \
	curl -fsSL https://pecl.php.net/get/redis --ipv4 | tar xvz -C "/usr/src/php/ext/redis" --strip 1; \
	docker-php-ext-install redis;

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Node
RUN apt-get install -y nodejs npm


RUN groupadd -g 1000 laravel
RUN useradd -u 1000 -ms /bin/bash -g laravel user

COPY --chown=user:laravel . /var/www/html/projeto

USER user

CMD ["php-fpm"]
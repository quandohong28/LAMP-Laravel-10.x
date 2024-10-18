FROM php:8.2-apache

# Cài đặt các extension PHP cần thiết
RUN apt-get update && apt-get install -y \
    libpng-dev \
    libjpeg-dev \
    libfreetype6-dev \
    zip \
    unzip \
    git \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd pdo pdo_mysql

# Cài đặt Composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Kích hoạt module Apache mod_rewrite
RUN a2enmod rewrite

# Cài đặt Node.js (nếu cần thiết)
RUN curl -sL https://deb.nodesource.com/setup_22.x | bash - \
    && apt-get install -y nodejs

# Copy file cấu hình Apache
COPY ./docker/apache/vhost.conf /etc/apache2/sites-available/000-default.conf

# Cài đặt thư viện Laravel
WORKDIR /var/www/html

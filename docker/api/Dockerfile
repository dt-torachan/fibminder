FROM php:8.2-fpm-bullseye

# PHP-FPMの設定ファイルを設置
COPY www.conf /usr/local/etc/php-fpm.d/www.conf

# 依存ライブラリのインストール
RUN apt-get update && apt-get install -y \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    libonig-dev \
    zip \
    unzip \
    git \
    && docker-php-ext-install -j$(nproc) iconv \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd

# Laravelに必要なPHP拡張のインストール
RUN docker-php-ext-install pdo pdo_mysql mbstring

# Composerのインストール
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# オプション: xdebugインストール (開発環境でのデバッグに使用)
# RUN pecl install xdebug && docker-php-ext-enable xdebug

WORKDIR /var/www
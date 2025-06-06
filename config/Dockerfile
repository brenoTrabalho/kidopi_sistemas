# Base PHP 5.6 com Apache
FROM php:5.6-apache

# Corrige os repositórios antigos do Debian
RUN sed -i 's/deb.debian.org/archive.debian.org/g' /etc/apt/sources.list && \
    sed -i 's|security.debian.org|archive.debian.org|g' /etc/apt/sources.list && \
    echo "Acquire::Check-Valid-Until false;" > /etc/apt/apt.conf.d/99no-check-valid-until && \
    sed -i '/stretch-updates/d' /etc/apt/sources.list

# Instala dependências
RUN apt-get update && apt-get install -y --allow-unauthenticated \
    libfreetype6-dev \
    libjpeg-dev \
    libpng-dev \
    libssl-dev \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install gd mysqli \
    && rm -rf /var/lib/apt/lists/*

# Ativa mod_rewrite do Apache
RUN a2enmod rewrite

# Instala extensão mongo antiga (compatível com PHP 5.6)
RUN pecl channel-update pecl.php.net && \
    pecl install mongo-1.6.16 && \
    docker-php-ext-enable mongo

# Remove configuração antiga do xdebug se existir
RUN rm -f /usr/local/etc/php/conf.d/xdebug.ini || true

# Instalação limpa do Xdebug 2.5.5
RUN pecl channel-update pecl.php.net && \
    pecl install xdebug-2.5.5 && \
    docker-php-ext-enable xdebug

# Define diretório padrão do Apache
WORKDIR /var/www/html

# Copia configuração do xdebug
COPY ./php/xdebug.ini /usr/local/etc/php/conf.d/xdebug.ini
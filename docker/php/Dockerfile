FROM php:8.2-fpm-alpine
LABEL MAINTAINER="Vagner Cardoso <vagnercardosoweb@gmail.com>"

# Environments
ENV TZ=America/Sao_Paulo
ENV WORKDIR=/var/www/app.dev

# Updates and installs system dependencies
RUN apk add --update --no-cache \
    zip \
    unzip \
    bash \
    tzdata \
    libxml2-dev \
    libpng-dev \
    libwebp-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    postgresql-dev \
    libzip-dev \
    libxslt-dev \
    oniguruma-dev \
    linux-headers \
    $PHPIZE_DEPS && \
    rm -rf /var/cache/apk/*

# Configure php dependency
RUN docker-php-ext-configure soap --enable-soap
RUN docker-php-ext-configure gd --enable-gd --with-freetype --with-jpeg --with-webp

# Install php dependencies
RUN docker-php-ext-install \
    -j$(nproc) gd \
    bcmath \
    xml \
    soap \
    mbstring \
    pdo \
    pdo_mysql \
    pdo_pgsql \
    mysqli \
    zip \
    opcache \
    intl \
    xsl \
    exif

# Install lib from pecl
RUN pecl channel-update pecl.php.net \
    && pecl install -o -f xdebug \
    && pecl install -o -f redis \
    && docker-php-ext-enable xdebug redis \
    && rm -rf /tmp/pear

# Install composer
COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

# Copy php settings
COPY ./conf.d ${PHP_INI_DIR}/conf.d

# Workdir
RUN mkdir -p ${WORKDIR}
WORKDIR ${WORKDIR}

# Expose port
EXPOSE 9000

# Copy entrypoint
COPY ./entrypoint.sh /usr/bin/docker-entrypoint
RUN chmod +x /usr/bin/docker-entrypoint

# Start
CMD [ "docker-entrypoint" ]

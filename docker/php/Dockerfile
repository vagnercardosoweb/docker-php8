FROM php:8-fpm-alpine

# Workdir
ENV WORKDIR=/home/app
WORKDIR ${WORKDIR}

# Updates and installs system dependencies
RUN apk add --update --no-cache \
    bash \
    tzdata \
    libxml2-dev \
    libpng-dev \
    libjpeg-turbo-dev \
    freetype-dev \
    postgresql-dev \
    libzip-dev \
    libxslt-dev \
    oniguruma-dev \
    $PHPIZE_DEPS && \
    rm -rf /var/cache/apk/*

# Timezone
ENV TZ=America/Sao_Paulo
RUN echo date.timezone = $TZ > ${PHP_INI_DIR}/conf.d/docker-php-ext-timezone.ini

# Configure php dependency
RUN docker-php-ext-configure soap --enable-soap
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

# Install php dependencies
RUN docker-php-ext-install \
  -j$(nproc) gd \
  iconv \
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
  exif \
  soap

# Install xdebug
RUN pecl install xdebug \
 && docker-php-ext-enable xdebug \
 && echo 'xdebug.start_with_request=no' >> ${PHP_INI_DIR}/conf.d/xdebug.ini \
 && echo 'xdebug.mode=debug' >> ${PHP_INI_DIR}/conf.d/xdebug.ini \
 && echo 'xdebug.client_host=host.docker.internal' >> ${PHP_INI_DIR}/conf.d/xdebug.ini \
 && echo 'xdebug.client_port=9000' >>  ${PHP_INI_DIR}/conf.d/xdebug.ini \
 && echo 'xdebug.remote_cookie_expire_time=36000' >>  ${PHP_INI_DIR}/conf.d/xdebug.ini

# Install extension redis
RUN pecl -v install redis
RUN docker-php-ext-enable redis

# Install extension rar
RUN pecl -v install rar
RUN docker-php-ext-enable rar

# Copy php settings
COPY ./php.ini ${PHP_INI_DIR}/conf.d/99-php.ini

# Install composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Copy files to container
#COPY . ${WORKDIR}

# Installs composer dependencies
#RUN cd ${WORKDIR}/applcation && composer install -o

# Expose port 9000 and start php-fpm server
EXPOSE 9000

CMD ["php-fpm"]

FROM php:8-apache

# Timezone
ENV TZ=America/Sao_Paulo
RUN echo $TZ > /etc/timezone
RUN dpkg-reconfigure -f noninteractive tzdata
RUN echo date.timezone = $TZ > /usr/local/etc/php/conf.d/docker-php-ext-timezone.ini

# Atualiza e instala dependências do sistema
RUN  apt-get update \
  && apt-get upgrade -y \
  && apt-get autoremove -y \
  && apt-get install -yq \
  zlib1g-dev \
  libzip-dev \
  libpq-dev \
  libmcrypt-dev \
  libpng-dev \
  libjpeg62-turbo-dev \
  libfreetype6-dev \
  libicu-dev \
  libxml2-dev \
  libxslt-dev \
  libnotify-bin \
  libwebp-dev \
  libxpm-dev \
  libonig-dev \
  unixodbc \
  unixodbc-dev \
  freetds-dev \
  freetds-bin \
  tdsodbc \
  zip \
  unzip \
  git \
  curl \
  vim \
  gnupg \
  && apt-get clean; rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Configura dependencia do php
RUN docker-php-ext-configure pdo_dblib --with-libdir=/lib/x86_64-linux-gnu
RUN docker-php-ext-configure soap --enable-soap
RUN docker-php-ext-configure gd --with-freetype --with-jpeg

# Instala dependencias do php
RUN docker-php-ext-install \
  gd \
  iconv \
  bcmath \
  xml \
  soap \
  mbstring \
  pdo \
  pdo_mysql \
  pdo_pgsql \
  pdo_dblib \
  mysqli \
  zip \
  opcache \
  intl \
  xsl \
  exif

# Instala composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug \
  && docker-php-ext-enable xdebug \
  && echo 'xdebug.start_with_request=yes' >> /usr/local/etc/php/conf.d/xdebug.ini \
  && echo 'xdebug.mode=debug' >> /usr/local/etc/php/conf.d/xdebug.ini \
  && echo 'xdebug.client_host=host.docker.internal' >> /usr/local/etc/php/conf.d/xdebug.ini \
  && echo 'xdebug.client_port=9000' >>  /usr/local/etc/php/conf.d/xdebug.ini \
  && echo 'xdebug.remote_cookie_expire_time=36000' >>  /usr/local/etc/php/conf.d/xdebug.ini

# Install redis
RUN pecl install redis
RUN docker-php-ext-enable redis

# Instala rar
# RUN pecl -v install rar
# RUN docker-php-ext-enable rar

# Cria certificado SSL
RUN openssl req -new -x509 -days 365 -nodes \
  -out /etc/ssl/certs/ssl-cert-snakeoil.pem \
  -keyout /etc/ssl/private/ssl-cert-snakeoil.key \
  -subj "/CN=*.localhost"

# Apache config
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2ensite default-ssl
RUN echo "ServerName docker" >> /etc/apache2/apache2.conf

# Permissão de usuários
RUN usermod -u 1000 www-data
RUN chown www-data:1000 -R /var/www/

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

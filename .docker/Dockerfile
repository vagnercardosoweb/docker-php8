FROM php:7.4-apache

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
  -j$(nproc) gd \
  json \
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
  exif \
  soap

# Instala composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Install xdebug
RUN pecl install xdebug
RUN docker-php-ext-enable xdebug
RUN echo "xdebug.remote_enable=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini &&\
    echo "xdebug.remote_connect_back=1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini &&\
    echo "xdebug.idekey=\"PHPSTORM\"" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini &&\
    echo "xdebug.remote_port=9001" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Instala rar
# RUN pecl -v install rar
# RUN docker-php-ext-enable rar

# Cria certificado SSL
RUN openssl req -new -x509 -days 365 -nodes \
  -out /etc/ssl/certs/ssl-cert-snakeoil.pem \
  -keyout /etc/ssl/private/ssl-cert-snakeoil.key \
  -subj "/CN=*.localhost"

# Habilita modulos e site
RUN a2enmod rewrite
RUN a2enmod ssl
RUN a2ensite default-ssl

# Permissão de usuários
RUN usermod -u 1000 www-data
RUN chown www-data:1000 -R /var/www/

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

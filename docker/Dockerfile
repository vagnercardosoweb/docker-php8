FROM php:7.2-apache

# Atualiza e instala dependências
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
  unixodbc \
  unixodbc-dev \
  freetds-dev \
  freetds-bin \
  tdsodbc \
  curl \
  git \
  vim \
  sudo \
  gnupg \
  && rm -rf /var/lib/apt/lists/*

# Instala dependencia do php
RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
RUN docker-php-ext-configure pdo_dblib --with-libdir=/lib/x86_64-linux-gnu
RUN docker-php-ext-install \
  gd \
  json \
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
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
  && php -r "copy('https://composer.github.io/installer.sig', 'installer.sig');" \
  && php -r "if (hash_file('SHA384', 'composer-setup.php') === trim(file_get_contents('installer.sig'))) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); unlink('installer.sig');} echo PHP_EOL;" \
  && php composer-setup.php --install-dir=/usr/local/bin --filename=composer \
  && php -r "unlink('composer-setup.php'); unlink('installer.sig');"

# Configura rar e xdebug
RUN pecl -v install rar xdebug
RUN docker-php-ext-enable rar
RUN docker-php-ext-enable xdebug

# Habilita modulos do apache
RUN a2enmod rewrite
RUN a2enmod ssl

# Cria certificado SSL
RUN openssl req -new -x509 -days 365 -nodes \
    -out /etc/ssl/certs/ssl-cert-snakeoil.pem \
    -keyout /etc/ssl/private/ssl-cert-snakeoil.key \
    -subj "/C=BR/ST=Paraná/L=Umuarama/O=VCWeb Networks/CN=*.localhost"

# Habilita o certificado SSL
RUN a2ensite default-ssl

# Permissão de usuários
RUN usermod -u 1000 www-data
RUN chown www-data:1000 -R /var/www/

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]

# Docker com PHP 8

Caso não tenha é preciso instalar o docker e docker-compose.

- [Instalar Docker](https://docs.docker.com/install/)
- [Instalar Docker Compose](https://docs.docker.com/compose/install/)

Depois de instalar basta rodar no terminal na raiz aonde está o arquivo `docker-compose.yml` o seguinte comando.

```bash
docker-compose up -d
```

**-d** significa que será executado em background e seu terminal não irá ficar travado e para matar o processo basta
apertar `CTRL + C` no windows ou `Command + C` no mac.

## Images pré configuradas

- [Nginx](https://www.nginx.com/)
- [Apache2](https://httpd.apache.org/)
- [MySQL](https://www.mysql.com/)
- [MariaDB](https://mariadb.com/)
- [PhpMyAdmin](https://www.phpmyadmin.net/)
- [PostgreSQL](https://www.postgresql.org/)
- [Redis](https://redis.io/)
- [PHP 8 FPM](https://php.net/)
  - [PHP Modules]
    - bcmath
    - Core
    - ctype
    - curl
    - date
    - dom
    - exif
    - fileinfo
    - filter
    - ftp
    - gd
    - hash
    - iconv
    - intl
    - json
    - libxml
    - mbstring
    - mysqli
    - mysqlnd
    - openssl
    - pcre
    - PDO
    - pdo_mysql
    - pdo_pgsql
    - pdo_sqlite
    - Phar
    - posix
    - rar
    - readline
    - redis
    - Reflection
    - session
    - SimpleXML
    - soap
    - sodium
    - SPL
    - sqlite3
    - standard
    - tokenizer
    - xdebug
    - xml
    - xmlreader
    - xmlwriter
    - xsl
    - Zend OPcache
    - zip
    - zlib

  - [Zend Modules]
    - Xdebug
    - Zend OPcache

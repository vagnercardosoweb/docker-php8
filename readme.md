# Docker PHP 7.4 + Apache2 + Mysql + PostgreSQL

Caso não tenha é preciso instalar o docker e docker-compose.

- [Instalar Docker](https://docs.docker.com/install/)
- [Instalar Docker Compose](https://docs.docker.com/compose/install/)

Depois de instalar basta rodar no terminal na raiz aonde está o arquivo `docker-compose.yml` o seguinte comando.

```bash
docker-compose up -d
```

**-d** significa que será executado em background e seu terminal não irá ficar travado e para matar o processo basta apertar `CTRL + C` no windows ou `Command + C` no mac.

## Dependências

- [Apache2](https://httpd.apache.org/) v2.4+
- [PHP](https://php.net/) v7.4+

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
    - pdo_dblib
    - pdo_mysql
    - pdo_pgsql
    - pdo_sqlite
    - Phar
    - posix
    - readline
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

- [MySQL](https://www.mysql.com/) v5.7.26
- [PostgreSQL](https://www.postgresql.org/) \*

Aproveite!

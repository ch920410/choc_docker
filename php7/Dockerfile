FROM centos:centos7
MAINTAINER choc<qinghecao@outlook.com>

ENV TZ "Asia/Shanghai"
ENV PHP_VERSION='7.2.0'

RUN groupadd php && useradd -g php php

RUN yum -y update && \
    yum install -y gcc automake autoconf libtool make gcc-c++ wget openssl-devel zip vim unzip net-tools

RUN yum install -y libxml2 libxml2-devel openssl openssl-devel curl-devel libjpeg-devel libpng-devel freetype-devel libmcrypt-devel bzip2 bzip2-devel gmp gmp-devel readline readline-devel libxslt libxslt-devel && \
    yum clean all

RUN cd /tmp/ && \
    wget "http://cn2.php.net/get/php-${PHP_VERSION}.tar.gz/from/this/mirror" && \
    tar -zxf mirror && \
    cd "php-${PHP_VERSION}" && \
    ./configure \
    --prefix=/usr/local/php7 \
    --exec-prefix=/usr/local/php7 \
    --bindir=/usr/local/php7/bin \
    --sbindir=/usr/local/php7/sbin \
    --includedir=/usr/local/php7/include \
    --libdir=/usr/local/php7/lib/php \
    --mandir=/usr/local/php7/php/man \
    --with-config-file-path=/usr/local/php7/etc \
    --enable-fpm \
    --enable-inline-optimization \
    --disable-debug \
    --disable-rpath \
    --enable-shared \
    --enable-soap \
    --with-libxml-dir \
    --with-xmlrpc \
    --with-openssl \
    --with-mhash \
    --with-pcre-regex \
    --with-sqlite3 \
    --with-zlib \
    --enable-bcmath \
    --with-iconv \
    --with-bz2 \
    --enable-calendar \
    --with-curl \
    --with-cdb \
    --enable-dom \
    --enable-exif \
    --enable-fileinfo \
    --enable-filter \
    --with-pcre-dir \
    --enable-ftp \
    --with-gd \
    --with-openssl-dir \
    --with-jpeg-dir \
    --with-png-dir \
    --with-zlib-dir \
    --with-freetype-dir \
    --enable-gd-jis-conv \
    --with-gettext \
    --with-gmp \
    --with-mhash \
    --enable-json \
    --enable-mbstring \
    --enable-mbregex \
    --enable-mbregex-backtrack \
    --with-libmbfl \
    --with-onig \
    --enable-pdo \
    --with-mysqli=mysqlnd \
    --with-pdo-mysql=mysqlnd \
    --with-zlib-dir \
    --with-pdo-sqlite \
    --with-readline \
    --enable-session \
    --enable-shmop \
    --enable-simplexml \
    --enable-sockets \
    --enable-sysvmsg \
    --enable-sysvsem \
    --enable-sysvshm \
    --enable-wddx \
    --with-libxml-dir \
    --with-xsl \
    --enable-zip \
    --enable-mysqlnd-compression-support \
    --with-pear \
    --enable-opcache  && \
    make && \
    make install

RUN ln -sf /usr/local/php7/bin/php    /usr/local/bin/php && \
    ln -sf /usr/local/php7/bin/phpize /usr/local/bin/phpize && \
    ln -sf /usr/local/php7/bin/pecl   /usr/local/bin/pecl

RUN cp "/tmp/php-${PHP_VERSION}/php.ini-development" /usr/local/php7/etc/php.ini && \
    cp /usr/local/php7/etc/php-fpm.conf.default /usr/local/php7/etc/php-fpm.conf && \
    cp /usr/local/php7/etc/php-fpm.d/www.conf.default /usr/local/php7/etc/php-fpm.d/www.conf

RUN php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');" && \
    php composer-setup.php && \
    php -r "unlink('composer-setup.php');" && \
    mv composer.phar /usr/local/bin/composer

EXPOSE 9000

ENTRYPOINT ["/usr/local/php7/sbin/php-fpm", "-F", "-c", "/usr/local/php7/etc/php.ini"]

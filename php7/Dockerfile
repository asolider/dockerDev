# 拉取 CentOS
FROM centos:7

ARG php_version

ENV PATH=$PATH:/opt/php/bin/:/opt/php/sbin/

# 安装依赖
RUN set -x \
  && curl -fsSL -o /etc/yum.repos.d/CentOS-Base.repo https://mirrors.aliyun.com/repo/Centos-7.repo \
  && yum install epel-release -y \
  #&& yum update -y \
  && yum -y install pcre pcre-devel zlib zlib-devel openssl openssl-devel libxml2 libxml2-devel libjpeg libjpeg-devel \
      libpng libpng-devel curl curl-devel libicu libicu-devel libmcrypt  libmcrypt-devel freetype freetype-devel \
      libmcrypt libmcrypt-devel bzip2-devel  gmp-devel autoconf gcc-c++ gcc wget make automake cmake \
      libevent libevent-devel cyrus-sasl cyrus-sasl-devel oniguruma-devel

RUN set -x \
  && mkdir /opt/download \
  && cd /opt/download \
  \
  && wget -O php.tar.gz "http://php.net/get/php-${php_version}.tar.gz/from/this/mirror" \
  && mkdir -p /opt/download/php \
  && tar -zxvf php.tar.gz -C /opt/download/php --strip-components=1 \
  \
  && cd php \
  && ./configure \
    --prefix=/opt/php \
    --enable-fpm \
    --with-config-file-path=/opt/php/etc \
    --with-config-file-scan-dir=/opt/php/etc/scan.d \
    --with-openssl \
    --with-zlib \
    --enable-bcmath \
    --with-bz2 \
    --enable-calendar \
    --with-curl \
    --enable-exif \
    --with-gd \
    --with-jpeg-dir \
    --with-png-dir \
    --with-freetype-dir \
    --enable-gd-native-ttf \
    --with-gettext \
    --with-mhash \
    --with-gmp \
    --enable-intl \
    --enable-mbstring \
    --with-mcrypt \
    --with-mysqli=mysqlnd \
    --enable-opcache \
    --enable-pcntl  \
    -with-pdo-mysql=mysqlnd \
    --enable-soap \
    --enable-sockets \
    --enable-zip \
    --without-sqlite3 \
    --without-pdo-sqlite \
  && make && make install \
  && yum clean all && rm -rf /var/cache/yum/* \
  && cp /opt/download/php/php.ini-development /opt/php/etc/php.ini \
  && cp /opt/php/etc/php-fpm.conf.default /opt/php/etc/php-fpm.conf \
  && cp /opt/php/etc/php-fpm.d/www.conf.default /opt/php/etc/php-fpm.d/www.conf
RUN set -x \
# lib memcached
  && cd /opt/download/ \
  && wget -O /opt/download/libmemcached.tar.gz "https://launchpad.net/libmemcached/1.0/1.0.18/+download/libmemcached-1.0.18.tar.gz" \
  && mkdir -p /opt/download/libmemcached \
  && tar -zxvf /opt/download/libmemcached.tar.gz -C /opt/download/libmemcached --strip-components=1 \
  && cd /opt/download/libmemcached \
  && ./configure && make && make install \
  \
  && wget -O /opt/download/php-memcached.tar.gz "https://github.com/php-memcached-dev/php-memcached/archive/v3.1.5.tar.gz" \
  && mkdir -p /opt/download/php-memcached \
  && tar -zxvf /opt/download/php-memcached.tar.gz -C /opt/download/php-memcached --strip-components=1 \
  && cd /opt/download/php-memcached \
  && phpize \
  && ./configure && make && make install \
  && sed -i '/If you wish to have an extension loaded/i extension=memcached.so' /opt/php/etc/php.ini \
# lib redis
  && wget -O /opt/download/php-redis.tar.gz "https://github.com/phpredis/phpredis/archive/4.3.0.tar.gz" \
  && mkdir -p /opt/download/php-redis \
  && tar -zxvf /opt/download/php-redis.tar.gz -C /opt/download/php-redis --strip-components=1 \
  && cd /opt/download/php-redis \
  && phpize \
  && ./configure && make && make install \
  && sed -i '/If you wish to have an extension loaded/i extension=redis.so' /opt/php/etc/php.ini \
  \
  && rm -rf /opt/download

CMD ["php-fpm", "-y", "/opt/php/etc/php-fpm.conf", "-F"]
EXPOSE 9000


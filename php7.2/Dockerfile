# 拉取 CentOS
FROM centos:7

ARG php7_version

# 安装依赖
RUN set -x \
  && yum install epel-release -y \
  && yum update -y \
  && yum -y install pcre pcre-devel zlib zlib-devel openssl openssl-devel libxml2 libxml2-devel libjpeg libjpeg-devel \
      libpng libpng-devel curl curl-devel libicu libicu-devel libmcrypt  libmcrypt-devel freetype freetype-devel \
      libmcrypt libmcrypt-devel bzip2-devel  gmp-devel autoconf gcc-c++ gcc wget make automake cmake \

  && mkdir /opt/download \
  && cd /opt/download \

  && wget -O php.tar.gz "http://php.net/get/php-${php7_version}.tar.gz/from/this/mirror" \
  && mkdir -p /opt/download/php \
  && tar -zxvf php.tar.gz -C /opt/download/php --strip-components=1 \

  && cd php \
  && ./configure \
    --prefix=/opt/php7 \
    --enable-fpm \
    --with-config-file-path=/opt/php7/etc \
    --with-config-file-scan-dir=/opt/php7/etc/scan.d \
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
    --with-gettext \
    --with-mhash \
    --with-gmp \
    --enable-intl \
    --enable-mbstring \
    --with-mysqli=mysqlnd \
    --enable-opcache \
    --enable-pcntl  \
    -with-pdo-mysql=mysqlnd \
    --enable-soap \
    --enable-sockets \
    --enable-zip \
  && make && make install \
  && yum clean all && rm -rf /var/cache/yum/* \
  && ln -s /opt/php7/bin/php /usr/local/bin/php \
  && ln -s /opt/php7/bin/phpize /usr/local/bin/phpize \
  && ln -s /opt/php7/sbin/php-fpm /usr/local/bin/php-fpm \
  && cp /opt/download/php/php.ini-development /opt/php7/etc/php.ini \
  && cp /opt/php7/etc/php-fpm.conf.default /opt/php7/etc/php-fpm.conf \
  && cp /opt/php7/etc/php-fpm.d/www.conf.default /opt/php7/etc/php-fpm.d/www.conf \
  && rm -rf /opt/download

CMD ["php-fpm", "-y", "/opt/php7/etc/php-fpm.conf", "-F"]
EXPOSE 9000


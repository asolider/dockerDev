FROM centos:7

ARG redis_version

RUN set -x \
	&& yum update -y \
	&& yum install -y tar wget gcc make \

	&& mkdir /opt/download \
	&& cd /opt/download \

	&& wget -O redis.tar.gz "http://download.redis.io/releases/redis-$redis_version.tar.gz" \
	&& mkdir -p /opt/download/redis \
	&& tar -zxvf redis.tar.gz -C /opt/download/redis --strip-components=1 \

	&& cd redis \
	&& make MALLOC=libc && make PREFIX=/usr/local/redis install \
	&& yum clean all && rm -rf /var/cache/yum/* \
	&& rm -rf /opt/download

EXPOSE 6379

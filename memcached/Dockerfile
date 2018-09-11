FROM centos:7

ARG memcached_version

RUN set -x \
	&& yum update -y \
	&& yum install -y libevent-devel libevent tar wget gcc make \

	&& mkdir /opt/download \
	&& cd /opt/download \

	&& wget -O memcached.tar.gz "http://memcached.org/files/memcached-$memcached_version.tar.gz" \
	&& mkdir -p /opt/download/memcached \
	&& tar -zxvf memcached.tar.gz -C /opt/download/memcached --strip-components=1 \

	&& cd memcached \
	&& ./configure && make && make install \
	&& yum clean all && rm -rf /var/cache/yum/* \
	&& rm -rf /opt/download

EXPOSE 11211

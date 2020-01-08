FROM debian:stretch-slim
# Debian version 9.* (slim)

COPY ./bin/* /usr/local/bin

RUN set -eux ;\
	sed -i 's/^#\s*\(deb.*main restricted\)$/\1/g' /etc/apt/sources.list ;\
	sed -i 's/^#\s*\(deb.*universe\)$/\1/g' /etc/apt/sources.list ;\
	sed -i 's/^#\s*\(deb.*multiverse\)$/\1/g' /etc/apt/sources.list ;\
	\
	export DEBIAN_FRONTEND="noninteractive" ;\
	apt-get dist-upgrade --assume-yes ;\
	apt-get update ;\
	apt-get install --assume-yes --no-install-recommends apt-utils ;\
## workaround for issue https://github.com/dotcloud/docker/issues/1024 \
	dpkg-divert --local --rename --add /sbin/initctl ;\
	ln -sf /bin/true /sbin/initctl ;\
	\
## workaround for issue https://bugs.launchpad.net/launchpad/+bug/974584 \
	dpkg-divert --local --rename --add /usr/bin/ischroot ;\
	ln -sf /bin/true /usr/bin/ischroot ;\
	\
## install support for apt-get-repository \
	apt-get install --assume-yes --no-install-recommends \
		apt-transport-https \
		ca-certificates \
		software-properties-common \
		gnupg2 \
	;\
## install commonly used tools \
	apt-get install --assume-yes --no-install-recommends \
		logrotate \
		vim \
		curl \
	;\
## clean installation \
	dckr-clean ;\
	set +eux ;


CMD ["bin/bash"]

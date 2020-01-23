FROM ubuntu:18.04 AS ubuntu-builder
LABEL maintainer="Joaquín Cuenca Abela <joaquin@freepik.com>"

ENV NGINX_VERSION 1.15.6
ENV MOD_JDOMAIN_DIR /opt/nginx/modules/http-upstream-jdomain

RUN apt-get update
RUN apt-get install -y dpkg-dev software-properties-common wget
RUN add-apt-repository -s -y ppa:nginx/development
RUN sed -i -e 's/# deb-src/deb-src/g' /etc/apt/sources.list && \
	apt-get update
RUN mkdir -p /opt/nginx && \
	cd /opt/nginx && \
	chown -R _apt:root . && \
	apt-get source nginx
RUN apt-get build-dep -y nginx

# Download third-parties modules
RUN mkdir -p ${MOD_JDOMAIN_DIR} && \
	wget https://github.com/e98cuenc/ngx_upstream_jdomain/archive/master.tar.gz && \
	tar xzvf master.tar.gz -C ${MOD_JDOMAIN_DIR} --strip-components=1

RUN cd /opt/nginx/nginx-${NGINX_VERSION} && \
	sed -i -e 's@^common_configure_flags := @common_configure_flags := --add-module='"${MOD_JDOMAIN_DIR}"' @' debian/rules && \
	dpkg-buildpackage -b
CMD ["bash"]

FROM ubuntu:18.04 AS nginx
COPY --from=ubuntu-builder \
	/opt/nginx/nginx-common*.deb \
	/opt/nginx/nginx-common*.ddeb \
	/opt/nginx/nginx-extras*.deb \
	/opt/nginx/nginx-extras*.ddeb \
	/opt/nginx/libnginx-mod-*.deb \
	/opt/nginx/libnginx-mod-*.ddeb \
	/opt/
RUN apt update && apt install -y /opt/*.deb /opt/*.ddeb && \
	cp -R /etc/nginx/modules-enabled /usr/share/nginx/modules-enabled && \
	mkdir /var/cache/nginx && \
	rm -f /var/cache/apt/archives/*.deb /var/cache/apt/archives/partial/*.deb /var/cache/apt/*.bin && \
	rm -rf /var/lib/apt/lists/* && \
	rm -f /opt/*
EXPOSE 80
STOPSIGNAL SIGTERM
ENTRYPOINT ["nginx"]
CMD ["-g", "daemon off;"]

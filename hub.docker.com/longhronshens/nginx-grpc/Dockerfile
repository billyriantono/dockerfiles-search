FROM ubuntu:16.04

ADD . /app

RUN apt-get update \
	&& apt-get install --no-install-recommends --no-install-suggests -y libgd3 libxslt1.1 libvpx3 libxpm4 libgeoip1 libssl1.0.0 \
	&& rm -rf /var/lib/apt/lists/*

WORKDIR /app
	
RUN dpkg -i nginx-common_1.13.5-0ubuntu0.16.04.4_all.deb
RUN dpkg -i nginx-full_1.13.5-0ubuntu0.16.04.4_amd64.deb

EXPOSE 80

STOPSIGNAL SIGTERM

VOLUME /usr/local/nginx/conf

CMD ["nginx", "-g", "daemon off;"]
FROM 1and1internet/debian-9
MAINTAINER brian.wilkinson@fasthosts.co.uk
ARG DEBIAN_FRONTEND=noninteractive
COPY files /
ENV PASSENGER_APP_ENV=production \
	SSL_KEY=/ssl/ssl.key \
	SSL_CERT=/ssl/ssl.crt

RUN \
	apt-get update -q && \
	apt-get install -y dirmngr gnupg && \
	apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 561F9B9CAC40B2F7 && \
	apt-get install -q -o Dpkg::Options::=--force-confdef -y apt-transport-https ca-certificates && \
	echo "deb https://oss-binaries.phusionpassenger.com/apt/passenger stretch main" > /etc/apt/sources.list.d/passenger.list && \
	apt-get update -yq && \
	apt-get install -q -o Dpkg::Options::=--force-confdef -y libnginx-mod-http-passenger nginx-extras ssl-cert \
															 sqlite3 libmariadbclient-dev-compat mysql-common && \
	apt-get autoremove -q -y && \
	apt-get clean -q -y && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/www/html && \
	rm -rf /var/www && \
	mkdir -p /var/www && \
	chmod -R 777 /var/www /var/log/nginx /var/lib/nginx && \
	chmod -R 755 /hooks /init /etc/ssl/private && \
	chmod 777 /etc/passwd /etc/group /etc && \
	touch /var/log/nginx/access.log /var/log/nginx/error.log && \
	chmod -R 777 /var/log/nginx/ && \
	echo "" >> /etc/nginx/nginx.conf && \
	echo "daemon off;" >> /etc/nginx/nginx.conf && \
	mkdir -p /etc/nginx/main.d/ && \
	sed -i -e 's|http {|include /etc/nginx/main.d/*;\nhttp {|' /etc/nginx/nginx.conf && \
	chmod -R 777 /etc/nginx/sites-enabled && \
	/usr/bin/passenger-config validate-install  --auto --no-colors
EXPOSE 8080 8443
WORKDIR /var/www

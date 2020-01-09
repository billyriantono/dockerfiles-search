# using Debian 9.5
FROM halvardssm/debian:latest 
ADD VERSION .
RUN { \
		echo mysql-community-server mysql-community-server/data-dir select ''; \
		echo mysql-community-server mysql-community-server/root-pass password ''; \
		echo mysql-community-server mysql-community-server/re-root-pass password ''; \
		echo mysql-community-server mysql-community-server/remove-test-db select false; \
	} | debconf-set-selections && \
    apt install -y nginx mysql-server php-fpm php-mysql 
EXPOSE 80
ENV NAME lemp
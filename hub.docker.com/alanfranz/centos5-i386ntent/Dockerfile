FROM wordpress
MAINTAINER Rumen LISHKOV "rumenlishkoff@gmail.com"

COPY ./apache2-foreground /usr/local/bin/
RUN apt update && apt install nano net-tools sudo -y && \
	curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
	chmod +x wp-cli.phar && \
	mv wp-cli.phar /usr/sbin/wp && \
	chmod +x /usr/local/bin/apache2-foreground
EXPOSE 80
WORKDIR /app
CMD ["apache2-foreground"]

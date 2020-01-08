FROM wordpress:4.8.3-php5.6-apache


RUN apt-get update && apt-get install -y less

####Wordpress CLI
RUN curl -O https://raw.githubusercontent.com/wp-cli/builds/gh-pages/phar/wp-cli.phar && \
mv wp-cli.phar /usr/local/bin/wp && \
chmod +x /usr/local/bin/wp

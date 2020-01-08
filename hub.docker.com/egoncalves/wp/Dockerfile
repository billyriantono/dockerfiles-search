FROM wordpress:php7.1-apache

# install the PHP extensions we need
RUN	apt-get update; apt-get install -y git; \
	rm -rf /var/lib/apt/lists/*

LABEL   br.com.egoncalves="Eduardo Gonçalves" \
        version="1.0" \
        description="Wordpress with Git"

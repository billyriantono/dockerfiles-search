FROM nginx:latest

RUN apt-get update \
    && apt-get --assume-yes --quiet install wget \
    && apt-get --assume-yes --quiet install ntpdate ntp unzip whois curl wamerican-huge \
	&& apt-get --assume-yes --quiet install php-fpm php-sqlite3 php-curl

RUN mkdir mkdir -p /var/www/html/noipfraud \
    && wget -O /tmp/install.zip "http://cdn2.noipfraud.com/noipfraud-client-1.8.zip" \
	&& unzip -o /tmp/install.zip -d /var/www/html/noipfraud \
	&& rm /tmp/install.zip 
	
RUN mkdir -p /var/www/html/noipfraud/api/db

ADD ./web/* /var/www/html/
ADD ./nginx/default.conf /etc/nginx/conf.d/default.conf

RUN usermod -aG www-data www-data \
    && chown -R www-data:www-data /var/www/html \
    && chmod 2775 /var/www/html \
	&& echo "Done"
	
CMD ["nginx", "-g", "daemon off;"]
FROM nextcloud:apache

RUN apt-get update && apt-get install -y smbclient && rm -rf /var/lib/apt/lists/*
RUN usermod -u 1000 www-data
RUN groupmod -g 1000 www-data
RUN chown -R 1000:1000 /var/www/html

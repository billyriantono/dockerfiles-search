FROM vitr/nginx-php-fpm:latest

COPY ./app /var/www/html

EXPOSE 443 80

WORKDIR "/var/www/html"
CMD ["/start.sh"]

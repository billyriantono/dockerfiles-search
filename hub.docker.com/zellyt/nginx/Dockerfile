FROM nginx:1.14.2
LABEL maintainer="Zellyt IT <it@zellyt.com>"

COPY files/nginx/nginx.conf /etc/nginx/nginx.conf
COPY files/nginx/sites/ etc/nginx/sites-available
COPY files/nginx/conf.d/ /etc/nginx/conf.d

WORKDIR /var/www

# Setting persmissions
RUN chown -R :www-data .

CMD ["nginx"]

EXPOSE 80 443
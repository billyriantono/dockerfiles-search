###### QNIBng image
FROM qnib/nginx

RUN dnf install -y php-fpm
ADD etc/nginx/nginx.conf /etc/nginx/
ADD etc/supervisord.d/php-fpm.ini /etc/supervisord.d/
ADD etc/consul.d/fpm.json /etc/consul.d/

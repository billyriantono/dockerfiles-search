FROM ubuntu 
#ke thua images ubuntu
MAINTAINER Phanbook <hello@gsviec.com> 
#thong tin nguoi quan ly

# run update and install nginx, php-fpm and other useful libraries
RUN apt-get update -y && \
	apt-get install -y \
	php-fpm php-mysql
#khi ban mu?n luu tru data trên máy local
VOLUME ["/var/www/html"]
#khi run bash vao docker thi no lam viec voi thu muc do'
WORKDIR /var/www/html
#Port d?ch v? ch?y
EXPOSE 9000
#cau lenh khoi tao

CMD ["php-fpm.0"]

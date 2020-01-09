FROM nginx
MAINTAINER kris "kris@sina.com"
ADD https://www.baidu.com/img/bd_logo1.png?where=super  /usr/share/nginx/html/
RUN echo 'Hello Docker!!!'>/usr/share/nginx/html/index.html \
	&& cd /usr/share/nginx/html/ \
	&& chmod 666 bd_logo1.png
COPY ./01.html /usr/share/nginx/html/

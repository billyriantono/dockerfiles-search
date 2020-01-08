FROM maxexcloo/nginx:latest
MAINTAINER Qi Zhang <todayhill@gmail.com>
ADD nginx.conf /etc/nginx/
ADD default.conf /etc/nginx/host.d/
ADD supervisord.conf /etc/supervisor/conf.d/nginx.conf
EXPOSE 80

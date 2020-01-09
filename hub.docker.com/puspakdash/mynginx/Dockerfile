FROM ubuntu:latest
MAINTAINER "Puspak Dash"
RUN apt-get update && \
        apt-get install -y nginx wget && apt-get clean && \
	rm -rf /tmp/* /var/tmp/* && rm -f /var/www/html/*.html
EXPOSE 8081-8089
COPY index.html /var/www/html/index.html
VOLUME ["/var/log/nginx"]
CMD nginx -g 'daemon off;' 

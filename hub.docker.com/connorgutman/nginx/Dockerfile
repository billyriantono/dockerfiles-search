FROM stackbrew/ubuntu:14.04
MAINTAINER Connor Gutman "connorgutman@gmail.com"
RUN apt-get update -qq && apt-get -y install nginx
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN mkdir /etc/nginx/ssl
ADD default /etc/nginx/sites-available/default
ADD default-ssl /etc/nginx/sites-available/default-ssl

EXPOSE 80

CMD ["nginx"]

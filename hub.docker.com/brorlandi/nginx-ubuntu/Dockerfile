FROM ubuntu:14.04

MAINTAINER Bruno Orlandi, brorlandi@gmail.com

RUN apt-get update
RUN apt-get install -y vim

RUN apt-get install -y software-properties-common \
      python-software-properties && \
    add-apt-repository -y ppa:nginx/stable && apt-get update && \
    apt-get -y install nginx

RUN rm -v /etc/nginx/nginx.conf
ADD nginx.conf /etc/nginx/

EXPOSE 80

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
CMD service nginx start

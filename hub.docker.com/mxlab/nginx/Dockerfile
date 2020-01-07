# Nginx - Ubuntu 14.04

FROM mxlab/ubuntu-base
MAINTAINER Maxime Lacour <dockerhub@lacour-maxime.fr>

RUN apt-get update && apt-get install -y nginx && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN rm /etc/nginx/nginx.conf
ADD nginx.conf /etc/nginx/nginx.conf

VOLUME ["/etc/nginx/sites-enabled"]

EXPOSE 80

CMD ["nginx"]

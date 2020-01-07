# Base from official nginx image
FROM nginx

MAINTAINER Alexandros Sapranidis<alexsapran@gmail.com>

# explicitly set user/group IDs
RUN usermod -u 1000 www-data

WORKDIR /var/
COPY ./nginx.conf /etc/nginx/nginx.conf

# Expose logs so other containers (e.g. logstash-forwarder) can process them
VOLUME ["/var/log/nginx", "/var/www/html"]

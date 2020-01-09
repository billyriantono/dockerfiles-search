FROM debian:jessie

MAINTAINER "Julien 'Tyloo' Bonvarlet" <jbonva@gmail.com>

# We add the official Nginx repository
RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
RUN echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list

# We set the Nginx version
ENV NGINX_VERSION 1.9.0-1~jessie

# We fetch Nginx
RUN apt-get update -y && apt-get install -y ca-certificates nginx=${NGINX_VERSION} && rm -rf /var/lib/apt/lists/*

# Apply Nginx configuration
ADD config/nginx.conf /etc/nginx/
ADD config/app.dev /etc/nginx/sites-available/
RUN mkdir -p /etc/nginx/sites-enabled
RUN ln -s /etc/nginx/sites-available/app.dev /etc/nginx/sites-enabled/app.dev

# Forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/app.dev-access.log
RUN ln -sf /dev/stderr /var/log/nginx/app.dev-error.log

# Add user to www-data group
RUN usermod -u 1000 www-data

# Command Handler
CMD ["nginx"]

# PORTS
EXPOSE 80

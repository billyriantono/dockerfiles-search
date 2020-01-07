FROM samtayuk/base:14.04
MAINTAINER Samuel Taylor "samtaylor.uk@gmail.com"

ENV NGINX_VERSION 1.9.10-1+trusty0

# Install Nginx
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C300EE8C \
    && echo "deb http://ppa.launchpad.net/nginx/development/ubuntu trusty main" >> /etc/apt/sources.list \
    && apt-get update \
    && apt-get install -y -q --no-install-recommends \ 
      ca-certificates \
      nginx=${NGINX_VERSION} \
      gettext-base \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /etc/nginx/sites-enabled/default

# Configure Nginx and apply fix for long server names and Pass all docker environment
RUN echo "daemon off;" >> /etc/nginx/nginx.conf \
  && sed -i 's/^http {/&\n    server_names_hash_bucket_size 64;/g' /etc/nginx/nginx.conf

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

CMD ["nginx"]
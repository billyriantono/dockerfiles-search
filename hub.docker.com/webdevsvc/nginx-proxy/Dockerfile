# Base image
FROM jwilder/nginx-proxy

# Base dependencies
RUN apt-get update \
  && apt-get install -y \
    curl \
  && rm -rf /var/lib/apt/lists/*

# Configurations
ADD ./configs/post_size.conf /etc/nginx/conf.d/post_size.conf
ADD ./configs/proxy.conf /etc/nginx/proxy.conf
ADD ./configs/timeout.conf /etc/nginx/conf.d/timeout.conf

# Expose ports
EXPOSE 80

# Healthcheck
ADD ./docker-healthcheck.sh /usr/local/bin/docker-healthcheck
RUN chmod +x /usr/local/bin/docker-healthcheck
HEALTHCHECK CMD docker-healthcheck

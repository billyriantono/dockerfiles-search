FROM ubuntu:trusty

ENV DEBIAN_FRONTEND noninteractive

#################################################
# NGINX

# Install PPA dependencies
RUN \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get -y install \
    software-properties-common

# Add nginx PPA
RUN \
  apt-add-repository -y ppa:nginx/stable

# Update apt cache with PPA
RUN \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get -y install \
    nginx-full && \
  rm -rf /var/lib/apt/lists/*

# Remove unused dependencies
RUN \
  apt-get remove --purge -y \
    software-properties-common &&\
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

VOLUME ["/var/cache/nginx"]

#################################################

CMD ["nginx", "-g", "daemon off;"]

FROM debian:8.3

# https://docs.docker.com/engine/userguide/eng-image/dockerfile_best-practices/
# You should avoid RUN apt-get upgrade or dist-upgrade, as many of the “essential” packages
# from the base images won’t upgrade inside an unprivileged container.
#RUN apt-get update && apt-get -y dist-upgrade
RUN apt-get update && apt-get -y install \
    apt-utils \
    libterm-readline-perl-perl \
    vim-nox \
    wget \
&& apt-get clean

# Nginx repo
RUN wget http://nginx.org/keys/nginx_signing.key
RUN apt-key add nginx_signing.key
RUN rm nginx_signing.key
RUN echo "deb http://nginx.org/packages/debian/ jessie nginx" >> /etc/apt/sources.list
RUN echo "deb-src http://nginx.org/packages/debian/ jessie nginx" >> /etc/apt/sources.list
RUN apt-get update && apt-get -y install nginx

COPY entrypoint.sh /sbin
RUN chmod +x /sbin/entrypoint.sh

#RUN /sbin/entrypoint.sh
#ENTRYPOINT ["nginx", "-g", "daemon off;"]

# Expose Nginx
EXPOSE 80/tcp

ENTRYPOINT ["/sbin/entrypoint.sh"]

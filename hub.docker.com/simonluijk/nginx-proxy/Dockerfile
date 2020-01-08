FROM debian:jessie
MAINTAINER simon@simonluijk.com

ENV DEBIAN_FRONTEND noninteractive
ENV REFRESHED_AT 2015-06-04
RUN echo 'DPkg::Post-Invoke {"/bin/rm -f /var/cache/apt/archives/*.deb || true";};' | tee /etc/apt/apt.conf.d/no-cache && \
    apt-get update -y && \
    apt-get dist-upgrade -y && \
    apt-get clean && \
    rm -rf /var/cache/apt/*

RUN apt-get install -y nginx && \
    rm -rf /var/lib/apt/lists/* && \
    sed -i -e '1idaemon off;' /etc/nginx/nginx.conf

ADD proxy.conf /etc/nginx/sites-enabled/default

EXPOSE 80
CMD ["nginx"]

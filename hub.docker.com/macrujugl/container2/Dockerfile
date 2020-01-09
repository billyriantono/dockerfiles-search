FROM debian:unstable
MAINTAINER marienza@gmail.com

ENV DEBIAN_FRONTEND noninteractive
ENV LANG en_US.UTF-8

RUN apt-get -y update -q -o Acquire::Pdiffs=false && \
    apt-get -y install -q locales && \
    echo en_US.UTF-8 UTF-8 > /etc/locale.gen && \
    dpkg-reconfigure -f noninteractive locales && \
    echo "Europe/Madrid" > /etc/timezone && \
    dpkg-reconfigure -f noninteractive tzdata && \
    sed -i "s/#precedence ::ffff:0:0\/96  100/precedence ::ffff:0:0\/96  100/g" /etc/gai.conf

# nginx
# forward request and error logs to docker log collector
RUN apt-get -y update && \
    apt-get -y install nginx-light && \
    ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

RUN mkdir -p /usr/local/share/grafana

COPY default /etc/nginx/sites-enabled/default

RUN apt-get -y autoclean && \
    apt-get -y --purge autoremove && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/*

ENV HOME /root
WORKDIR /root

EXPOSE 80
CMD ["/usr/sbin/nginx","-g","daemon off;"]

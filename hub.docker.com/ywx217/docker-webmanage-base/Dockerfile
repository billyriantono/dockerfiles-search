FROM ywx217/docker-netdata:latest
MAINTAINER Wenxuan Yang "ywx217@gmail.com"

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        shellinabox \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN useradd user && echo 'user:user' | chpasswd
EXPOSE 9002
COPY shellinabox.conf /etc/supervisor/conf.d/shellinabox.conf

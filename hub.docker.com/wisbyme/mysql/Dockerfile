FROM mysql:5.7.27

LABEL maintainer="ljjun<wisbyme@gmail.com>"

COPY ./Hong_Kong /tmp/Hong_Kong

ENV FORCE_UNSAFE_CONFIGURE 1

RUN apt-get update \
    && apt-get upgrade -y --force-yes \
    && mkdir -p /usr/share/zoneinfo/Asia \ 
    && mv /tmp/Hong_Kong /usr/share/zoneinfo/Asia/Hong_Kong \
    && rm -rf /etc/localtime \
    && ln -s /usr/share/zoneinfo/Asia/Hong_Kong /etc/localtime \
    && apt-get autoremove -y \
    && apt-get autoclean -y \
    && rm -rf /var/cache/apt/* /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 3306

FROM ubuntu:xenial
MAINTAINER Alex Salt <alex.salt@e96.ru>

ADD https://github.com/kreuzwerker/envplate/releases/download/v0.0.8/ep-linux /usr/local/bin/ep

RUN apt-get update -qq \
    && apt-get install --no-install-recommends -y \
    collectd libpython2.7 \
    && chmod +x /usr/local/bin/ep \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ADD collectd.conf /etc/collectd/
ADD entry.sh /

ENTRYPOINT [ "/entry.sh" ]
CMD [ "collectd", "-f", "-C", "/etc/collectd/collectd.conf" ]

FROM hopsoft/graphite-statsd:0.9.12-phusion
MAINTAINER Chuck Sakoda <chuck.sakoda@us.imshealth.com>

ENV CARBON_UDP_ENABLED True
RUN mkdir -p /etc/my_init.d
ADD scripts/01-carbon_udp.sh /etc/my_init.d/
ADD files/storage-schemas.conf /opt/graphite/conf/
ADD files/local_settings.py /opt/graphite/webapp/graphite/local_settings.py
RUN rm -f /opt/graphite/conf/*.example

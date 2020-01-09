FROM python:3.4

MAINTAINER Sean H "sahsu.mobi@gmail.com"

ENV OPENVPN_MONITOR_VERSION master
ENV HOST 127.0.0.1
ENV PORT 5555
RUN wget -q https://github.com/furlongm/openvpn-monitor/archive/${OPENVPN_MONITOR_VERSION}.tar.gz -O openvpn-monitor-${OPENVPN_MONITOR_VERSION}.tar.gz \
 && tar -xvzf openvpn-monitor-${OPENVPN_MONITOR_VERSION}.tar.gz \
 && mv openvpn-monitor-${OPENVPN_MONITOR_VERSION} /srv/openvpn-monitor \
 && rm /openvpn-monitor-${OPENVPN_MONITOR_VERSION}.tar.gz

RUN mkdir -p /usr/share/GeoIP/ \
  && cd /usr/share/GeoIP \
  && wget http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz \
  && gunzip GeoLiteCity.dat.gz \
  && mv GeoLiteCity.dat GeoIPCity.dat

RUN mkdir -p /srv/openvpn-monitor

WORKDIR /srv/openvpn-monitor
RUN pip install -r requirements.txt \
  && pip install gunicorn

COPY openvpn-monitor.conf ./


COPY entrypoint.sh /sbin/entrypoint.sh
RUN chmod 755 /sbin/entrypoint.sh
ENTRYPOINT ["/sbin/entrypoint.sh"]

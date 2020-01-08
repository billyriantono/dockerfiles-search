FROM docker.elastic.co/logstash/logstash:5.4.1
USER root
RUN mkdir /opt/maxmind
RUN curl -LO "http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz" && \
    gunzip GeoLiteCity.dat.gz && \
    mv GeoLiteCity.dat /opt/maxmind
# GeoIp database /opt/maxmind/GeoLiteCity.dat
USER logstash

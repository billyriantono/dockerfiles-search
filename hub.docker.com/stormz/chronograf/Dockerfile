from buildpack-deps:jessie-curl

ENV VERSION 0.12.0
ENV CHRONOGRAF_BIND 0.0.0.0:10000
ENV CHRONOGRAF_LOCAL_DATABASE /data/chronograf.db

RUN wget https://s3.amazonaws.com/get.influxdb.org/chronograf/chronograf_${VERSION}_amd64.deb \
    && dpkg -i chronograf_${VERSION}_amd64.deb \
    && rm chronograf_${VERSION}_amd64.deb

EXPOSE 10000
VOLUME ["/data"]

CMD ["/opt/chronograf/chronograf", "-config", "/opt/chronograf/config.toml"]

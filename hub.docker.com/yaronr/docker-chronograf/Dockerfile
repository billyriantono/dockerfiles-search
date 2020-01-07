FROM multicloud/debian-wheezy
MAINTAINER yaronr

ENV CHRONOGRAPH_VERSION=0.10.0-1

RUN wget --progress=bar:force --no-check-certificate https://s3.amazonaws.com/get.influxdb.org/chronograf/chronograf_0.10.0_amd64.deb -O /tmp/chronograf_latest_amd64.deb && \
  dpkg -i /tmp/chronograf_latest_amd64.deb && \
  rm /tmp/chronograf_latest_amd64.deb && \
  rm -rf /var/lib/apt/lists/*

EXPOSE 10000

ENTRYPOINT ["/opt/chronograf/chronograf"]

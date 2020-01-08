FROM debian:jessie

MAINTAINER Víctor González <victor.gonzalez@geomati.co>

ENV DEBIAN_FRONTEND noninteractive
ENV VERSION 5.23.0

RUN echo "deb http://httpredir.debian.org/debian jessie contrib" >> /etc/apt/sources.list
RUN set -x \
	&& apt-get update \
	&& apt-get install -yq wget exim4 \
  && rm -rf /var/lib/apt/lists/*

RUN sed -i "s#dc_eximconfig_configtype.*#dc_eximconfig_configtype='internet'#" /etc/exim4/update-exim4.conf.conf

RUN cd /usr/local/lib \
    && wget https://mmonit.com/monit/dist/binary/${VERSION}/monit-${VERSION}-linux-x64.tar.gz \
    && tar xzf monit-${VERSION}-linux-x64.tar.gz \
    && ln -s "/usr/local/lib/monit-${VERSION}/bin/monit" /usr/local/bin/monit

COPY monitrc /etc/monitrc

RUN chmod 0700 /etc/monitrc

ENTRYPOINT service exim4 start && monit -Ic /etc/monitrc

EXPOSE 2812


FROM debian:jessie
MAINTAINER Christophe Burki, christophe.burki@gmail.com

ENV CHRONOGRAF_VERSION 1.3.6.1

# Install system requirements
RUN apt-get update && apt-get install -y \
    locales

# Configure locales and timezone
RUN locale-gen en_US.UTF-8 en_GB.UTF-8 fr_CH.UTF-8
RUN cp /usr/share/zoneinfo/Europe/Zurich /etc/localtime
RUN echo "Europe/Zurich" > /etc/timezone

# telegraf install and config
ADD https://dl.influxdata.com/chronograf/releases/chronograf_${CHRONOGRAF_VERSION}_amd64.deb /tmp/chronograf_amd64.deb
RUN dpkg -i /tmp/chronograf_amd64.deb

# s6 install and config
COPY bin/* /usr/bin/
RUN chmod a+x /usr/bin/s6-*
COPY configs/etc/s6 /etc/s6/
RUN chmod a+x /etc/s6/.s6-svscan/finish /etc/s6/chronograf/run /etc/s6/chronograf/finish

EXPOSE 8888

CMD ["/usr/bin/s6-svscan", "/etc/s6"]

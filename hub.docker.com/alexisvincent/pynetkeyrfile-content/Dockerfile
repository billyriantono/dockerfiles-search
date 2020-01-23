# Browser Mob Proxy

FROM openjdk:8-jdk

#========================
# Miscellaneous packages
# Includes minimal runtime used for executing non GUI Java programs
#========================
RUN apt-get update && apt-get -qqy --no-install-recommends install \
    bzip2 \
    ca-certificates \
    sudo \
    unzip \
    wget \
	locales \
	&& localedef -f UTF-8 -i ru_RU ru_RU.UTF-8

ENV LANG ru_RU.UTF-8
ENV LC_ALL ru_RU.UTF-8
#Set RU TimeZone
ENV TZ "Europe/Moscow"
	
# BMP install
ENV BMP_VERSION 2.1.4
RUN wget -O browsermob-proxy.zip https://github.com/lightbody/browsermob-proxy/releases/download/browsermob-proxy-$BMP_VERSION/browsermob-proxy-$BMP_VERSION-bin.zip \
    && unzip -q /browsermob-proxy.zip \
    && rm -f /browsermob-proxy.zip

RUN mv /browsermob-proxy-$BMP_VERSION /browsermob-proxy

COPY start.sh /
RUN chmod +x /start.sh

# ENV VALUE
ENV BMP_PORT 9090
ENV PORT_RANGE 39500-39999
ENV TTL 600

CMD ["/start.sh"]

FROM ubuntu:18.04
MAINTAINER TIKI SRE <sre@tiki.vn>

ENV DEBIAN_FRONTEND=noninteractive TZ=Asia/Saigon

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
    && echo $TZ > /etc/timezone \
    && apt-get -qq -y update \
    && apt-get install -qq --no-install-recommends -y \
        curl jq vim-nox moreutils gettext-base supervisor \
        locales tzdata lsb-release software-properties-common libasound2 wget\
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget --quiet https://download.java.net/java/ga/jdk11/openjdk-11_linux-x64_bin.tar.gz \
    && echo '3784cfc4670f0d4c5482604c7c513beb1a92b005f569df9bf100e8bef6610f2e openjdk-11_linux-x64_bin.tar.gz' > openjdk-11-sha256sum.txt \
    && sha256sum -c openjdk-11-sha256sum.txt \
    && tar -xvzf openjdk-11_linux-x64_bin.tar.gz \
    && mkdir -p /opt/java \
    && mv jdk-11 /opt/java \
    && ln -s /opt/java/jdk-11/bin/java /bin/java


COPY config /etc
COPY entrypoint.sh /entrypoint.sh

WORKDIR /app/
CMD ["/entrypoint.sh"]

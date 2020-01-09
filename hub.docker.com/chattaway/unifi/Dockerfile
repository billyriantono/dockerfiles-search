FROM debian:stable-slim

RUN mkdir --parents /usr/share/man/man1

RUN apt-get update \
    && apt-get install --yes \
        binutils \
        libcap2 \
        curl \
        mongodb-server \
        openjdk-8-jre-headless \
        jsvc \
    && apt-get clean all

RUN curl -sLO https://dl.ubnt.com/unifi/5.10.20/unifi_sysvinit_all.deb
RUN dpkg --install unifi_sysvinit_all.deb
RUN rm -rf unifi_sysvinit_all.deb

CMD ["/usr/bin/java", "-jar", "/usr/lib/unifi/lib/ace.jar", "start"]

EXPOSE 8080 8443 8880 8843 6789 3478/udp

VOLUME ["/usr/lib/unifi/data"]

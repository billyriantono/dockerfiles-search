FROM jeanblanchard/java:jre-8
LABEL MAINTAINER Xing Chain <dev@chainid.io>
LABEL version="1.11.13"

ENV NRSVersion=1.11.13

RUN \
  apk update && \
  apk add wget gpgme && \
  mkdir /cid-boot && \
  mkdir /cid && \
  cd /

ADD scripts /cid-boot/scripts

VOLUME /cid
WORKDIR /cid-boot

ENV CIDNET mainnet		

COPY ./cid-main.properties /cid-boot/conf/
COPY ./cid-test.properties /cid-boot/conf/
COPY ./init-cid.sh /cid-boot/

EXPOSE 6969 6868 6789 9999 8888

CMD ["/cid-boot/init-cid.sh", "/bin/sh"]

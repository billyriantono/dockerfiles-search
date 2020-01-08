FROM frolvlad/alpine-glibc

MAINTAINER fanshunen <fanshunen@gmail.com>

RUN apk update && \
    apk add --no-cache libstdc++ wget && \
        mkdir -p /rrys && \
        mkdir -p /opt/work/store && \
        wget -q https://appdown.rrysapp.com/rrshareweb_centos7.tar.gz -O /rrys/rrshareweb_centos7.tar.gz && \
        tar zxvf /rrys/rrshareweb_centos7.tar.gz -C /rrys/ && \
        rm -rf /rrys/rrshareweb_centos7.tar.gz && \
        apk del wget

WORKDIR /
VOLUME ["/opt/work/store"]
EXPOSE 3001

CMD ["sh", "-c", "/rrys/rrshareweb/rrshareweb"]

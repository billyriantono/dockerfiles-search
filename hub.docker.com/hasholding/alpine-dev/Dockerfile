FROM alpine:latest
ENV container docker
MAINTAINER "Levent SAGIROGLU" <LSagiroglu@gmail.com>

RUN apk add --update --no-cache bash nano file git curl openssl openssh build-base ca-certificates tzdata && \
    update-ca-certificates && \
    cp /usr/share/zoneinfo/Europe/Istanbul /etc/localtime && \
    echo "Europe/Istanbul" >  /etc/timezone && \
    apk del tzdata	

VOLUME /workdir
WORKDIR /workdir	
	
CMD ["/bin/bash"]
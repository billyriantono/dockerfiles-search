FROM alpine:latest 
MAINTAINER "Levent SAGIROGLU" <LSagiroglu@gmail.com>
ARG VERSION=v0.10.10
RUN apk update && \
    apk upgrade && \
    apk add --update openssl && \
    apk add ca-certificates && \
	   update-ca-certificates

VOLUME /srv 
COPY srv /srv
COPY bin /bin
WORKDIR /bin
RUN wget https://github.com/mholt/caddy/releases/download/${VERSION}/caddy_${VERSION}_linux_amd64.tar.gz -O caddy.tar.gz
RUN tar -zxvf caddy.tar.gz  caddy
RUN rm caddy.tar.gz
    
ENV WEBSRV ""
 
EXPOSE 80 443 2015

ENTRYPOINT ["/bin/entrypoint.sh"]

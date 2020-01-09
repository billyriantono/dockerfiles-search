FROM alpine:latest 
MAINTAINER "Levent SAGIROGLU" <LSagiroglu@gmail.com>
ARG VERSION=0.9.3
ARG TIMEZONE=Europe/Istanbul


RUN apk add --update --no-cache openssl tar tzdata ca-certificates && \
       update-ca-certificates && \
       cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
       echo "${TIMEZONE}" >  /etc/timezone && \
       wget  --quiet --output-document=/tmp/vault.zip https://releases.hashicorp.com/vault/${VERSION}/vault_${VERSION}_linux_amd64.zip && \
       unzip /tmp/vault.zip -d /bin && \
    apk del tzdata  && \
    rm -f /tmp/vault.zip /var/cache/apk/*
	
VOLUME /srv 
COPY etc /etc

ENV ETCDCONF "/etc/vault.hcl" 

WORKDIR /bin

EXPOSE 8200

ENTRYPOINT ["/bin/vault", "server"]
CMD ["-config=/etc/vault.hcl"]
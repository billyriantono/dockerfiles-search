FROM docker.io/alpine:latest
MAINTAINER jieyang <admin@jevic.cn>

# Install selfsigned ca (optional)
# COPY <ca.crt> /etc/ssl/certs/<ca.pem>
# Install basic packages
RUN apk add --update bash libressl curl fping libcap && rm -rf /var/cache/apk/* && mkdir /opt

FROM ruby:2.3-alpine

COPY install_mc.sh /

RUN apk add --no-cache build-base libffi-dev nodejs openssl && \
    sh /install_mc.sh && rm /install_mc.sh

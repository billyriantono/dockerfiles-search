FROM alpine:3.8

ENV PACKAGES "gettext curl openssl ca-certificates"
RUN apk add --update $PACKAGES && rm -rf /var/cache/apk/*

ENV AWSCLI_VERSION "1.14.10"
ENV PACKAGES "groff less python py-pip jq"

RUN apk add --update $PACKAGES \
&& pip install --upgrade pip \
&& pip install awscli==$AWSCLI_VERSION \
&& apk --purge -v del py-pip \
&& rm -rf /var/cache/apk/*

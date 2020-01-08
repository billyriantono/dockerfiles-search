FROM alpine:3.4
MAINTAINER An Phung <an.phungle@gmail.com>

ENV OTP_VERSION="18.3.2-r0"

LABEL henho.alpine.version="3.4" \
      henho.erlang.version=$OTP_VERSION \
      henho.author.name="An Phung" \
      henho.author.email="an.phungle@gmail.com"

# Adapted from devicexx/emqttd

RUN set -x \
    && apk update \
    && apk --no-cache add \
        erlang=$OTP_VERSION \
        erlang-public-key \
        erlang-syntax-tools \
        erlang-erl-docgen \
        erlang-gs \
        erlang-observer \
        erlang-ssh \
        erlang-ose \
        erlang-cosfiletransfer \
        erlang-runtime-tools \
        erlang-os-mon \
        erlang-tools \
        erlang-cosproperty \
        erlang-common-test \
        erlang-dialyzer \
        erlang-edoc \
        erlang-otp-mibs \
        erlang-crypto \
        erlang-costransaction \
        erlang-odbc \
        erlang-inets \
        erlang-asn1 \
        erlang-snmp \
        erlang-erts \
        erlang-et \
        erlang-cosnotification \
        erlang-xmerl \
        erlang-typer \
        erlang-coseventdomain \
        erlang-stdlib \
        erlang-diameter \
        erlang-hipe \
        erlang-ic \
        erlang-eunit \
        erlang-webtool \
        erlang-mnesia \
        erlang-erl-interface \
        erlang-test-server \
        erlang-sasl \
        erlang-jinterface \
        erlang-kernel \
        erlang-orber \
        erlang-costime \
        erlang-percept \
        erlang-dev \
        erlang-eldap \
        erlang-reltool \
        erlang-debugger \
        erlang-ssl \
        erlang-megaco \
        erlang-parsetools \
        erlang-cosevent \
        erlang-compiler \
    && rm -rf /var/cache/apk/*


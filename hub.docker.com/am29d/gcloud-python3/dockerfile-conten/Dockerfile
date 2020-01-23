FROM alpine:3.8
MAINTAINER Alvaro Lizama <me@alvarolizama.net>
RUN apk --no-cache add -U musl musl-dev make openssh gcc git erlang erlang-crypto erlang-syntax-tools \
    erlang-inets erlang-ssl erlang-public-key erlang-asn1 erlang-sasl erlang-runtime-tools \
    erlang-erl-interface erlang-dev erlang-parsetools erlang-eunit erlang-tools erlang-ssh \
    erlang-xmerl elixir bash \
    && mix local.hex --force \
    && mix local.rebar --force

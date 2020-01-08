FROM josemrb/build-asdf:0.7.0-20190228
LABEL maintainer="Jose Miguel Rivero Bruno <work@josemrb.com>"

RUN asdf plugin-add erlang
ARG ERLANG_VERSION=21.3.2
RUN asdf install erlang $ERLANG_VERSION
RUN asdf global erlang $ERLANG_VERSION

RUN asdf plugin-add elixir
ARG ELIXIR_VERSION=1.8.1-otp-21
RUN asdf install elixir $ELIXIR_VERSION
RUN asdf global elixir $ELIXIR_VERSION

RUN \
      mix local.hex --force && \
      mix local.rebar --force

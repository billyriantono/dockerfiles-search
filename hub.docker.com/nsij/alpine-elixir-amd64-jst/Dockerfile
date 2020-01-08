FROM nsij/alpine-amd64-jst:latest
RUN apk update && apk upgrade
RUN apk add --update elixir \
erlang-crypto && \
rm -rf /var/cache/apk/*

RUN mix local.hex --force && \
mix local.rebar --force

CMD ["/bin/sh"]

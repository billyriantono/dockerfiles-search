FROM alpine:3.6
RUN apk add --update git nodejs nodejs-npm \
					 erlang-ssl erlang-crypto elixir \
					 erlang-parsetools erlang-syntax-tools
RUN mix do local.rebar, local.hex --force
CMD ["mix --help"]

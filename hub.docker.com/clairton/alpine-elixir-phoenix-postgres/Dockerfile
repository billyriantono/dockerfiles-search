FROM bitwalker/alpine-elixir-phoenix:1.6.6

MAINTAINER Clairton Rodrigo Heinzen <clairton.rodrigo@gmail.com>

# add postgresql-client
RUN apk add --update --no-cache postgresql-client

EXPOSE 4000

# The command to run when this image starts up
CMD mix phx.server

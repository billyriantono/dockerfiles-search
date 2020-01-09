FROM elixir:latest
MAINTAINER CarLabs Engineering <engineering@carlabs.com>

# 
COPY config /src/config
COPY config/config.exs.example /src/config/config.exs
COPY mix.exs /src/mix.exs
RUN cd /src; mix local.hex --force; mix deps.get

# Bundle app source
#COPY . /src

# Expose
#EXPOSE  8080

# Run
WORKDIR /src

CMD [ "mix" ]

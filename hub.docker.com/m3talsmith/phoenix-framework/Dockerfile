FROM m3talsmith/elixir

MAINTAINER m3talsmith <m3talsmith@gmail.com>

# Bring the system up to date
RUN apt-get update > /dev/null\
  && apt-get update -y > /dev/null

# Install nodejs
RUN curl -sL https://deb.nodesource.com/setup_5.x | bash - > /dev/null
RUN apt-get install -y nodejs > /dev/null

RUN mix local.hex > /dev/null\
  && mix archive.install https://github.com/phoenixframework/phoenix/releases/download/v1.0.3/phoenix_new-1.0.3.ez > /dev/null

CMD ["iex"]

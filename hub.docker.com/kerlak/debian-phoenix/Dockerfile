FROM kerlak/debian-elixir
MAINTAINER Juan Carlos Pazos Mandiá <jucapaman@gmail.com>

# DEBIAN-PHOENIX
RUN yes | mix local.hex
RUN yes | mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs

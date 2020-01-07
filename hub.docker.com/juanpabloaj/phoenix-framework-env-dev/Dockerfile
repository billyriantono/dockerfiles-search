FROM marcelocg/phoenix

RUN apt-get update
RUN apt-get install -y sudo
RUN apt-get install -y postgresql-client
RUN apt-get install -y vim
RUN apt-get install -y inotify-tools

RUN useradd -m phoe && adduser phoe sudo
RUN echo "phoe ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/phoe
RUN chmod 0440 /etc/sudoers.d/phoe

USER phoe
WORKDIR /home/phoe

RUN mix archive.install --force https://github.com/phoenixframework/archives/raw/master/phx_new.ez
RUN mix local.hex --force \
    && mix local.rebar --force

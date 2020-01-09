FROM elixir:1.9.4

SHELL ["/bin/bash", "-c"]

RUN touch ~/.bashrc && cd /tmp \
&& wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash \
&& source ~/.bashrc \
&& nvm install --lts \
&& apt update \
&& apt install -y inotify-tools

RUN mix local.hex --force && mix local.rebar --force && mix archive.install hex phx_new 1.4.10 --force

WORKDIR /work/

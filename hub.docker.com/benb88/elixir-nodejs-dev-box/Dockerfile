FROM debian:jessie

MAINTAINER ben@bencao.it

# Install Necessary libs
# Install Erlang, Elixir, Nodejs

RUN apt-get update && \
    apt-get install -y curl wget locales git && \
    wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && \
    dpkg -i erlang-solutions_1.0_all.deb && \
    curl -sL https://deb.nodesource.com/setup_5.x | bash - && \
    apt-get update && \
    apt-get install -y sudo zsh build-essential inotify-tools && \
    apt-get install -y erlang-dev erlang-parsetools elixir && \
    apt-get install -y nodejs && \
    apt-get clean

# setup utf-8 locale
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen && \
    locale-gen && \
    update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 LC_COLLATE=en_US.UTF-8 LC_CTYPE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 LC_COLLATE=en_US.UTF-8 LC_CTYPE=en_US.UTF-8

# create wheel group which can sudo without password
RUN groupadd wheel && \
    echo "%wheel ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Install Oh my zsh

RUN git clone git://github.com/robbyrussell/oh-my-zsh.git /root/.oh-my-zsh && \
    cp /root/.oh-my-zsh/templates/zshrc.zsh-template /root/.zshrc

# Enable Terminal Color

RUN echo "export TERM=xterm-256color" >> ~/.zshrc
ENV TERM xterm-256color

# Install Docker & Docker Compose

RUN curl -LSso /usr/local/bin/docker https://get.docker.com/builds/Linux/x86_64/docker-1.10.3 && \
    chmod +x /usr/local/bin/docker && \
    curl -LSso /usr/local/bin/docker-compose https://github.com/docker/compose/releases/download/1.6.2/docker-compose-Linux-x86_64 && \
    chmod +x /usr/local/bin/docker-compose

# Install Mix & Hex & Rebar & Phoenix

RUN mix local.hex --force && \
    mix hex.info && \
    mix local.rebar --force && \
    mix archive.install https://github.com/phoenixframework/phoenix/releases/download/v1.1.4/phoenix_new-1.1.4.ez

CMD /bin/bash

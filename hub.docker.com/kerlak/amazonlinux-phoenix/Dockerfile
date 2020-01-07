FROM kerlak/amazonlinux-elixir
MAINTAINER Juan Carlos Pazos Mandiá <jucapaman@gmail.com>

# PHOENIX
RUN yes | mix local.hex && \
    yes | mix archive.install https://github.com/phoenixframework/archives/raw/master/phx_new.ez && \
    wget https://nodejs.org/dist/v6.11.1/node-v6.11.1-linux-x64.tar.xz && \
    tar xJf node-v6.11.1-linux-x64.tar.xz && rm node-v6.11.1-linux-x64.tar.xz
ENV PATH=$PATH:/node-v6.11.1-linux-x64/bin:/usr/bin/
RUN npm install brunch -g

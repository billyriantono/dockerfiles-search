FROM ubuntu:xenial

RUN apt-get -y update
RUN apt-get -y install git curl wget vim
# install elixir
RUN wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb
RUN dpkg -i erlang-solutions_1.0_all.deb
RUN apt-get -y update
RUN apt-get -y install esl-erlang
RUN apt-get -y install elixir
# install npm
RUN apt-get install -y nodejs npm
RUN ln -s /usr/bin/nodejs /usr/bin/node
#RUN npm install -g n
#RUN n latest
#RUN npm update -g npm
# install inotify-tools
RUN apt-get install -y inotify-tools
# install phoenix
RUN mkdir app
WORKDIR /app
RUN echo Y | mix archive.install https://github.com/phoenixframework/archives/raw/master/phx_new.ez
ENTRYPOINT while true; do sleep 10; done

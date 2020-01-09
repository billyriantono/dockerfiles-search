FROM ubuntu:rolling

RUN apt-get update

# Pacchetti utili solo per i test in CI
RUN apt-get install -y xvfb curl
RUN curl -sLo /usr/local/bin/wait-for-it.sh https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh \
    && chmod +x /usr/local/bin/wait-for-it.sh

# Pacchetti necessari per la compilazione del progetto
RUN apt-get install -y g++
RUN apt-get install -y cmake
RUN apt-get install -y clang
RUN apt-get install -y clazy
RUN apt-get install -y qt5-default
RUN apt-get install -y libqt5serialport5-dev

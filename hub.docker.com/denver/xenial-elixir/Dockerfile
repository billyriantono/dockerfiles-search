FROM ubuntu:xenial

RUN set -xe \
    && apt update \
    && apt-get -y install wget build-essential git \
    && wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb \
    && dpkg -i erlang-solutions_1.0_all.deb

RUN set -xe \
    && apt-get -y update \
    && apt-get -y install esl-erlang \
    && apt-get -y install elixir

CMD ["iex"]

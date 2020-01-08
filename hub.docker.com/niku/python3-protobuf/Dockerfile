FROM debian:buster-backports

ENV HOME /app
WORKDIR $HOME

RUN mkdir -p $HOME && \
    apt-get update -qq && \
    apt-get install -t buster-backports -y \
                protobuf-compiler \
                python3-protobuf \
                python3-yaml

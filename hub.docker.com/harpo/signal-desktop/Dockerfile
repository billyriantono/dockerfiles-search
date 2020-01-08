FROM ubuntu:18.04

LABEL maintainer "Harpo Roeder <roederharpo@protonmail.ch>"

RUN apt-get update -y && apt-get install -y curl gpg

RUN curl -s https://updates.signal.org/desktop/apt/keys.asc | apt-key add - &&\
    echo "deb [arch=amd64] https://updates.signal.org/desktop/apt xenial main" | tee -a /etc/apt/sources.list.d/signal-xenial.list && \
    apt-get update -y && \
    apt-get install -y signal-desktop

ENTRYPOINT ["signal-desktop"]

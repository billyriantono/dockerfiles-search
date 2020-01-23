FROM debian:buster

RUN apt-get update \
    && apt-get install -y wget libx11-xcb1 libnode-dev libasound2

RUN wget https://github.com/greymass/eos-voter/releases/download/v0.7.11/linux-eos-voter-0.7.11-amd64.deb \
  && dpkg -i linux-eos-voter-0.7.11-amd64.deb \
  ; rm linux-eos-voter-0.7.11-amd64.deb

RUN apt-get install -fy

RUN useradd -m user

USER user
VOLUME /home/user/.config/eos-voter

CMD eos-voter

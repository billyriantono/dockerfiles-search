FROM ubuntu:latest
LABEL Vladimir Yu. Ivanov, inbox@vova-ivanov.info

RUN apt-get -y update && apt-get -y install make texlive-full
WORKDIR /opt/markup

ENTRYPOINT ["make"]

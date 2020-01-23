FROM ubuntu:latest

RUN apt-get update
RUN apt-get install wget -y
RUN wget https://repo-feed.flightradar24.com/linux_x86_64_binaries/fr24feed_1.0.18-5_amd64.tgz
RUN tar xvzf fr24feed_1.0.18-5_amd64.tgz


ENTRYPOINT [ "fr24feed_amd64/fr24feed" ]
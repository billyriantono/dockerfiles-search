FROM ubuntu:latest

WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y \
 resiprocate-turn-server \
 net-tools \
 nano

COPY start.sh .

run chmod +x start.sh

COPY reTurnServer.config users.txt /etc/reTurn/

CMD ./start.sh

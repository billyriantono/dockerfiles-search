FROM ubuntu
MAINTAINER Saprykin Oleg <sapr@ro.ru>
RUN apt-get update && apt-get install transmission-daemon -y
COPY settings.json /etc/transmission-daemon/
ENTRYPOINT service transmission-daemon start && bash 
EXPOSE 9091


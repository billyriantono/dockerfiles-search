FROM ubuntu:latest
MAINTAINER @heywoodlh

COPY merlinserver /usr/bin/merlinserver
RUN apt-get update &&\
	apt-get install python3 -y

CMD ["/usr/bin/merlinserver", "-i", "0.0.0.0"]

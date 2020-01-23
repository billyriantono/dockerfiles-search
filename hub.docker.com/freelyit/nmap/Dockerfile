FROM alpine

MAINTAINER Jean-Pierre Broeders <github@freelyit.nl>

RUN apk update && \
	apk add nmap

ENTRYPOINT ["nmap"]
CMD ["-h"]
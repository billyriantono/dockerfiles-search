FROM alpine

MAINTAINER Jean-Pierre Broeders <github@freelyit.nl>

RUN apk update && \
	apk add whois

ENTRYPOINT ["whois"]
CMD ["--help"]
FROM alpine

MAINTAINER Jean-Pierre Broeders <github@freelyit.nl>

RUN apk update && \
	apk add pingu

ENTRYPOINT ["ping"]
CMD ["--help"]
FROM debian:stable

MAINTAINER Jesper Wermuth<jwermuth@gmail.com>

RUN apt-get update && apt-get install -y ImageMagick && rm -rf /var/lib/apt/lists/*
USER 1000
WORKDIR /input
ENTRYPOINT ["convert"]
CMD ["-help"]

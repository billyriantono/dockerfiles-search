FROM debian:jessie

MAINTAINER "Dmitry Momot" <mail@dmomot.com>

RUN apt-get update -y && apt-get install php5-cli -y

ENTRYPOINT ["php"]

CMD ["--help"]

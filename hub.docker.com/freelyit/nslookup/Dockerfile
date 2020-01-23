FROM ubuntu

MAINTAINER Jean-Pierre Broeders <github@freelyit.nl>

RUN apt-get update \
    && apt-get install -y dnsutils

ENTRYPOINT ["nslookup", "-q=any"]
CMD ["--help"]
# damon/bro
FROM debian:jessie

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        less \
        ruby \
        rubygems \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean \
    && apt-get autoremove -y

RUN gem install bropages

ENTRYPOINT ["bro"]

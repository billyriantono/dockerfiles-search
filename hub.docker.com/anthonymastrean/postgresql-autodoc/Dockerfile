FROM debian:stretch-slim

LABEL maintainer "Anthony Mastrean <anthony.mastrean@gmail.com>"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        postgresql-autodoc \
    && rm -fr /var/cache/apt/* /var/lib/apt/lists/*

ENTRYPOINT ["postgresql_autodoc"]

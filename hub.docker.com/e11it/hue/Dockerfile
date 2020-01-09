FROM gethue/hue

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
  && apt-get install -y krb5-user \
  && rm -rf /var/lib/apt/lists/*

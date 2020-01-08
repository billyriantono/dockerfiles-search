FROM python:3.6.4-slim-jessie

RUN apt-get update && \
  apt-get dist-upgrade -y && \
  apt-get install -y libgdal-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists*

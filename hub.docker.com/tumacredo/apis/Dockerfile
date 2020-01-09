# To save build time would build from
# the previously build image
# To rebuild the container again from scratch
# replace the base image with python:2.7.12
FROM tumacredo/apis:latest

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY . /usr/src/app
RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 80

ENV  C_FORCE_ROOT=1

CMD ["/bin/sh", "./run.sh"]
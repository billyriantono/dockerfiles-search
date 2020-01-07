FROM python:2.7

MAINTAINER SG Finans <frontutvikling@sgfinans.no>

RUN apt-get update && apt-get install -y rsync
RUN pip install fabric

WORKDIR /app
VOLUME /app

ENTRYPOINT ["fab"]

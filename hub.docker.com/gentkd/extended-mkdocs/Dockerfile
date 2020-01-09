# This is a comment
FROM python:alpine3.9
MAINTAINER gentkd

ENV PLANTUML_VERSION 1.2019.6
ENV LANG en_US.UTF-8

RUN mkdir /opt/plantuml \
    && mkdir /root/workspace

COPY ext-mkdocs-sample /root/sample
COPY plantuml.sh /opt/plantuml/

RUN apk update && apk add --no-cache \
  graphviz \
  openjdk8 \
  gcc \
  musl-dev \
  jpeg-dev \
  zlib-dev \
  libffi-dev \
  cairo-dev \
  pango-dev \
  gdk-pixbuf-dev

RUN apk add --no-cache curl \
    && curl -L https://sourceforge.net/projects/plantuml/files/plantuml.${PLANTUML_VERSION}.jar/download -o /opt/plantuml/plantuml.jar \
    && apk del curl \
    && link /opt/plantuml/plantuml.sh /bin/plantuml

RUN pip install \
  mkdocs \
  mkdocs-material \
  plantuml-markdown \
  pymdown-extensions \
  pygments \
  mkdocs-pdf-export-plugin

# expors for mkdocs serve
EXPOSE 8000

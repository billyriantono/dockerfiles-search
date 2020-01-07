FROM digitalmagic/docker-java
USER root

RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 573BFD6B3D8FBC641079A6ABABF5BD827BD9BF62
RUN echo "deb http://nginx.org/packages/mainline/debian/ jessie nginx" >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get install --no-install-recommends --no-install-suggests -y ca-certificates nginx rsyslog-elasticsearch
RUN rm -rf /var/lib/apt/lists/*
RUN mkdir -p /etc/nginx/ssl
COPY ./elasticsearch.conf /etc/rsyslog.d/elasticsearch.conf.example

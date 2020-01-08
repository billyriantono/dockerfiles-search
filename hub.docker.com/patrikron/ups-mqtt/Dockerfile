FROM ruby:alpine

RUN apk add --no-cache mosquitto-clients bash

COPY ups /opt/ups
WORKDIR /opt
RUN chmod 777 /opt/ups

CMD ["/bin/bash", "-c", "/opt/ups"]
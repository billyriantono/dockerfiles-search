FROM debian:jessie-slim

MAINTAINER Daniel Watrous

RUN apt-get update && apt-get install -y curl vim python python-dev python-setuptools ca-certificates build-essential && easy_install pip && pip install python-openstackclient && pip install python-heatclient

VOLUME /stack
#ENV OS_CACERT /stack/cert-bundle.pem

CMD [ "/bin/bash"]

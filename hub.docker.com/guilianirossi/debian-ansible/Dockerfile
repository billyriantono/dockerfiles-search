FROM debian:jessie
MAINTAINER "Rossi Guiliani" <rossi@guiliani.me>

RUN apt-get update && apt-get upgrade -y && apt-get install -y python-pip python-dev libffi-dev libssl-dev && pip install --upgrade setuptools && pip install pyasn1==0.1.8 markupsafe ansible

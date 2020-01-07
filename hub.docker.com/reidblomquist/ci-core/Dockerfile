FROM jenkins:latest

USER root

RUN apt-get update  && apt-get install -y \
  libffi-dev \
  libssl-dev \
  python \
  python-dev \
  python-pip \
  build-essential \
  && pip install -U cffi ansible==1.9.6 markupsafe


USER jenkins

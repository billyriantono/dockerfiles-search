# This docker file will create a container using the latest official Ubuntu image and install Flask
# Created by rkiles on 7-9-2016
# Updated to clone the beeUpFront git repo


FROM ubuntu:latest
MAINTAINER Richard Kiles <rkiles@gdt.com>
RUN apt-get -y update && apt-get install -y \
  tar \
  git \
  curl \
  vim \
  wget \
  build-essential \
  python \
  python-dev \
  python-pip
RUN pip install flask
WORKDIR /tmp
RUN git clone https://github.com/rkiles/test.git
RUN mkdir -p /root/.ssh/
RUN mv /tmp/test/id_rsa /root/.ssh/id_rsa
RUN chmod 600 /root/.ssh/id_rsa
RUN ssh-keyscan github.com >> /root/.ssh/known_hosts
RUN echo "    IdentityFile /root/.ssh/id_rsa" >> /etc/ssh/ssh_config
RUN git clone git@github.com:GDT-Labs/beeUpFront.git
WORKDIR beeUpFront
#ENV FLASK_APP /tmp/beeUpFront/app.py
ENV FLAS_APP /tmp/beeUpFront/rktest.py
CMD python -m flask run --host=0.0.0.0

FROM python:2.7
MAINTAINER Fabio Hisamoto <fabio@99taxis.com>

RUN \
  apt-get update &&\
  apt-get install -y build-essential python-dev &&\
  apt-get autoremove -y &&\
  apt-get clean &&\
  rm -rf /var/lib/apt/lists/* /var/tmp/*

RUN \
  pip install --upgrade pip &&\
  pip install argparse &&\
  pip install boto==2.39.0 &&\
  pip install elasticsearch-curator==3.4.1 &&\
  pip install awscli==1.10.12 &&\
  pip install awsebcli==3.7.3

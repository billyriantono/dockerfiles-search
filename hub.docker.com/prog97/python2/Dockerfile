FROM python:2.7
MAINTAINER Prog24

RUN set -x && \
  apt-get update && \
  apt-get install -y vim less

# pip install
RUN pip install topia.termextract
RUN pip install nltk
RUN pip install enum
RUN pip install rake-nltk

WORKDIR /root

FROM mllg/circleci-r:latest
MAINTAINER "Michel Lang" michellang@gmail.com

RUN install2.r --deps=TRUE --ncpus=-1 mlr3 \
  && rm -rf /tmp/*

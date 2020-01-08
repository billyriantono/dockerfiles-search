FROM google/cloud-sdk
MAINTAINER Shun Yanaura

RUN wget https://get.docker.com/builds/Linux/x86_64/docker-latest -O /usr/bin/docker \
  && chmod +x /usr/bin/docker \
  && gcloud components update -q

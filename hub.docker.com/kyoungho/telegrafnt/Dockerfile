FROM debian:stretch
MAINTAINER zhiyuan.cai@gmail.com

RUN apt-get update && apt-get install -y curl gnupg
RUN echo "deb http://packages.cloud.google.com/apt cloud-sdk-stretch main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg |  apt-key add -
RUN apt-get update && apt-get install -y google-cloud-sdk && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["gcloud"]

FROM google/cloud-sdk

MAINTAINER Nam Chu Hoai <nambrot@gmail.com>

ENV VERSION v2.6.1
ENV FILENAME helm-${VERSION}-linux-amd64.tar.gz

WORKDIR /

ADD https://storage.googleapis.com/kubernetes-helm/${FILENAME} /tmp
COPY helm_install_or_upgrade /bin/

RUN tar -zxvf /tmp/${FILENAME} -C /tmp \
  && mv /tmp/linux-amd64/helm /bin/helm \
  && rm -rf /tmp

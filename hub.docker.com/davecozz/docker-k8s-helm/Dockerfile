FROM alpine

RUN apk --no-cache add ca-certificates \
  && update-ca-certificates

RUN wget -O /tmp/helm.tgz http://kubernetes-helm.storage.googleapis.com/helm-v2.5.0-linux-amd64.tar.gz \
  && tar xzf /tmp/helm.tgz --strip 1 -C /tmp \
  && mv /tmp/helm /usr/local/bin/ \
  && rm -rf /tmp/*
  
CMD helm

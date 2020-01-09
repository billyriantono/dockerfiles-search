FROM alpine:3.9

ENV HELM_VERSION=2.12.3

RUN apk update
RUN apk add ca-certificates socat wget tar
RUN rm -rf /var/cache/apk/*

RUN wget -O /tmp/helm.tgz https://storage.googleapis.com/kubernetes-helm/helm-v${HELM_VERSION}-linux-arm.tar.gz
RUN tar xvf /tmp/helm.tgz
RUN mv ./linux-arm/tiller /tiller
RUN rm -rf ./linux-arm /tmp/helm.tgz

EXPOSE 44134
USER nobody
ENTRYPOINT ["/tiller"]

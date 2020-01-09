ARG K8S_VERSION=1.10.3

FROM alpine:3.7

RUN apk add --no-cache wget
RUN wget https://github.com/kubernetes/cloud-provider-openstack/releases/download/v0.1.0/cloud-provider-openstack-v0.1.0-linux-amd64.tar.gz
RUN tar -zxvf cloud-provider-openstack-v0.1.0-linux-amd64.tar.gz linux-amd64/cinder-flex-volume-driver

FROM gcr.io/google-containers/hyperkube:v${K8S_VERSION}
ARG DRIVER_PATH=/usr/libexec/kubernetes/kubelet-plugins/volume/exec/cinder~cinder-flex-volume-driver/

RUN mkdir -p $DRIVER_PATH
COPY --from=0 /linux-amd64/cinder-flex-volume-driver $DRIVER_PATH

RUN apt-get update && apt-get install -y \
    file \
 && rm -rf /var/lib/apt/lists/*

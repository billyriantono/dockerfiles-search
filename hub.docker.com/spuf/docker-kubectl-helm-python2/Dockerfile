# based on 
# - https://github.com/docker-library/docker
# - https://github.com/linkyard/docker-helm
# - https://github.com/linkyard/concourse-helm-resource

FROM alpine:3.8 as build

ENV DOCKER_VERSION=18.09.0
ENV KUBERNETES_VERSION=1.11.3
ENV HELM_VERSION=2.11.0

RUN apk add --update --no-cache ca-certificates git

WORKDIR /

RUN apk add --update -t deps ca-certificates curl tar gzip

### 
# docker
RUN curl -fL -o docker.tgz "https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}.tgz" && \
    tar --extract --file docker.tgz --strip-components 1 --directory /tmp

# set up nsswitch.conf for Go's "netgo" implementation (which Docker explicitly uses)
RUN [ ! -e /etc/nsswitch.conf ] && echo 'hosts: files dns' > /etc/nsswitch.conf

# Docker often uses "modprobe -va foo bar baz"
RUN curl -fL -o /tmp/modprobe "https://raw.githubusercontent.com/docker-library/docker/master/modprobe.sh" && \
    chmod +x /tmp/modprobe

### 
# kubectl
RUN curl -fL -o /tmp/kubectl "https://storage.googleapis.com/kubernetes-release/release/v${KUBERNETES_VERSION}/bin/linux/amd64/kubectl" && \
    chmod +x /tmp/kubectl

### 
# helm
RUN curl -fL -o helm.tar.gz "http://storage.googleapis.com/kubernetes-helm/helm-v${HELM_VERSION}-linux-amd64.tar.gz" && \
    tar --extract --file helm.tar.gz --strip-components 1 --directory /tmp
    
    
# The image we keep
FROM alpine:3.8

RUN apk add --update --no-cache git ca-certificates python2

# Force stdin, stdout and stderr to be totally unbuffered
ENV PYTHONUNBUFFERED=true

COPY --from=build /tmp/docker /bin/docker
COPY --from=build /tmp/modprobe /bin/modprobe
COPY --from=build /etc/nsswitch.conf /etc/nsswitch.conf

COPY --from=build /tmp/kubectl /bin/kubectl

COPY --from=build /tmp/helm /bin/helm

CMD ["sh"]

FROM alpine:3.8
ENV KUBECTL_VERSION=v1.10.9 \
    SKAFFOLD_VERSION=v0.16.0 \
    KUSTOMIZE_VERSION=v1.0.9

ADD https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl /usr/local/bin/kubectl
ADD https://storage.googleapis.com/skaffold/releases/${SKAFFOLD_VERSION}/skaffold-linux-amd64 /usr/local/bin/skaffold

RUN apk add --update --no-cache \
      docker \
      git \
      curl && \
    opsys=linux && \
    curl -s https://api.github.com/repos/kubernetes-sigs/kustomize/releases/tags/${KUSTOMIZE_VERSION} | \
      grep browser_download | \
      grep $opsys | \
      cut -d '"' -f 4 | \
      xargs curl -O -L && \
    mv kustomize_*_${opsys}_amd64 kustomize && \
    mv ./kustomize /usr/local/bin && \
    chmod -R u+x /usr/local/bin/

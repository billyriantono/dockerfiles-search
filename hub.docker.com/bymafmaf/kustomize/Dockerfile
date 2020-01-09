FROM alpine:3.11

ENV KUSTOMIZE_VERSION 3.5.3

RUN wget -qO- https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize/v3.5.3/kustomize_v3.5.3_linux_amd64.tar.gz | tar -xvz -C /usr/local/bin/ && \
  chmod +x /usr/local/bin/kustomize

ENTRYPOINT [ "kustomize" ]

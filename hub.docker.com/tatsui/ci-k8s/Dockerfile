FROM python:3.6-stretch

ARG VERSION=2.0.3

RUN curl -o /usr/local/bin/kustomize -LO https://github.com/kubernetes-sigs/kustomize/releases/download/v${VERSION}/kustomize_${VERSION}_linux_amd64 && \
  chmod +x /usr/local/bin/kustomize
RUN curl -o /usr/local/bin/kubectl -LO https://storage.googleapis.com/kubernetes-release/release/v1.14.0/bin/linux/amd64/kubectl && \
  chmod +x /usr/local/bin/kubectl

FROM alpine:3.8
ENV KUBECTL_VERSION=1.15.0 \
    KUSTOMIZE_VERSION=3.1.0

WORKDIR /app

RUN apk add --no-cache \
      curl \
      wget \
      git

RUN curl -L https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl

RUN curl -L https://github.com/kubernetes-sigs/kustomize/releases/download/v${KUSTOMIZE_VERSION}/kustomize_${KUSTOMIZE_VERSION}_linux_amd64 -o /usr/local/bin/kustomize \
    && chmod +x /usr/local/bin/kustomize

CMD ["kustomize"]
FROM alpine:3.10

ARG KUBERNETES_VERSION=1.16.0
ARG KUSTOMIZE_VERSION=3.4.0

RUN apk add --no-cache curl jq
RUN curl -L -o /usr/local/bin/kubectl  https://storage.googleapis.com/kubernetes-release/release/v${KUBERNETES_VERSION}/bin/linux/amd64/kubectl && chmod +x /usr/local/bin/kubectl
RUN curl -LO https://github.com/kubernetes-sigs/kustomize/releases/download/kustomize%2Fv${KUSTOMIZE_VERSION}/kustomize_v${KUSTOMIZE_VERSION}_linux_amd64.tar.gz && \
    tar xzf kustomize_v${KUSTOMIZE_VERSION}_linux_amd64.tar.gz && \
    rm kustomize_v${KUSTOMIZE_VERSION}_linux_amd64.tar.gz && \
    mv kustomize /usr/local/bin/kustomize && \
    chmod +x /usr/local/bin/kustomize

RUN mkdir -p /opt/resource/
COPY assets/* /opt/resource/

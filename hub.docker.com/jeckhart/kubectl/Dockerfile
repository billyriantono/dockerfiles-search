FROM alpine:3.6

ENV KUBECTL_VERSION=stable

ENV HOME=/config

RUN set -x && \
    apk add --no-cache bash bash-completion curl ca-certificates && \
    if [ "${KUBECTL_VERSION}"="stable" ]; then \
      curl -L "https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl" -o /usr/local/bin/kubectl ;\
    else \
      curl -LO "https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl" -o /usr/local/bin/kubectl ;\
    fi && \
    chmod +x /usr/local/bin/kubectl && \
    adduser -D -h /config kubectl && \
    kubectl version --client && \
    echo 'if [ -f /etc/profile.d/bash_completion.sh ]; then source /etc/profile.d/bash_completion.sh; source <(kubectl completion bash) ; fi' >> ~/.bashrc

USER kubectl

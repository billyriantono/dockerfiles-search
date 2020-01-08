FROM docker:latest

# kubectl
ENV KUBECTL_VERSION="1.14.6"
RUN wget -O /usr/bin/kubectl "https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl" \
  && chmod +x /usr/bin/kubectl

# helm
ENV HELM_VERSION="2.14.3"
RUN wget https://storage.googleapis.com/kubernetes-helm/helm-v${HELM_VERSION}-linux-amd64.tar.gz \
  && tar -xvf helm-v${HELM_VERSION}-linux-amd64.tar.gz \
  && mv linux-amd64/helm /usr/bin \
  && chmod +x /usr/bin/helm \
  && rm -f /helm-v${HELM_VERSION}-linux-amd64.tar.gz \
  && helm init --client-only

# skaffold
ENV SKAFFOLD_VERSION="0.38.0"
RUN wget -O /usr/bin/skaffold https://storage.googleapis.com/skaffold/releases/v${SKAFFOLD_VERSION}/skaffold-linux-amd64 \
  && chmod +x /usr/bin/skaffold

ENV GIT_VERSION="2.22"
RUN apk add --no-cache git~=${GIT_VERSION}

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["sh"]

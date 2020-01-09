FROM debian

ARG HELM_VERSION

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y curl git && \
    apt-get clean && \
    curl -o /tmp/helm.tar.gz https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz && \
    tar xvzf /tmp/helm.tar.gz --strip-components=1 -C /bin && \
    chmod +x /bin/helm && \
    helm init -c && \
    helm plugin install https://github.com/lrills/helm-unittest && \
    helm plugin install https://github.com/chartmuseum/helm-push

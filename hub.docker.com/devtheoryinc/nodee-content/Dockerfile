FROM google/cloud-sdk:273.0.0-alpine

ARG HELM_VERSION="v2.14.2"
ENV HELM_VERSION=$HELM_VERSION

RUN gcloud components install kubectl \
    && wget -q https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz -O - | tar -xzO linux-amd64/helm > /usr/local/bin/helm \
    && chmod +x /usr/local/bin/helm

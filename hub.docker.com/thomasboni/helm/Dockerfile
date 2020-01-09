FROM lachlanevenson/k8s-helm:v2.14.1

ARG KUBECTL_VERSION=v1.15.0

ENV HELM_HOME /home/helm
WORKDIR /home/helm

# Upgrade & requirements installation
RUN apk update && apk upgrade && apk add bash \
    curl \
    gnupg \
    git

# Plugins installation
RUN mkdir $HELM_HOME/plugins \
    && helm plugin install https://github.com/databus23/helm-diff --version master \
    && helm plugin install https://github.com/futuresimple/helm-secrets

# Kubectl installation
RUN curl --output /bin/kubectl https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl \
    && chmod a+x /bin/kubectl

ENTRYPOINT [""]

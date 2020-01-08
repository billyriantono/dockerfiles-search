FROM alpine:latest

ENV OS=linux

# latest stable: curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt
ENV KUBECTL_VERSION=v1.13.4
ENV KUBECTL_ARCH=amd64

# https://cloud.google.com/sdk/docs/quickstart-linux
ENV GCLOUD_VERSION=237.0.0
ENV GCLOUD_SHA256SUM=10e08362e750581c6ff3866314ed439a1bb544755657b204bf719f68e03b4ba3
ENV GCLOUD_ARCH=x86_64

RUN apk --no-cache add \
      bash \
      git \
      git-bash-completion \
      docker \
      openssh-client \
      curl \
      bind-tools \
      netcat-openbsd \
      ca-certificates \
      postgresql-client \
      vim \
      python \
      python3 \
      py3-virtualenv \
      python3-dev \
      g++ \
      openjdk8-jre \
      jq

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN curl -o /root/.git-prompt.sh https://raw.githubusercontent.com/git/git/v2.19.0/contrib/completion/git-prompt.sh

RUN curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz && \
    echo "${GCLOUD_SHA256SUM}  google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz" > google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz.sha256 && \
    sha256sum -c google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz.sha256 && \
    tar xzf google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz  && \
    rm -f google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz && \
    rm -f google-cloud-sdk-${GCLOUD_VERSION}-${OS}-${GCLOUD_ARCH}.tar.gz.sha256 && \
    /google-cloud-sdk/bin/gcloud config set component_manager/disable_update_check true && \
    /google-cloud-sdk/bin/gcloud config set core/disable_usage_reporting true && \
    mkdir -p /usr/local/Caskroom/google-cloud-sdk/latest && \
    ln -s /google-cloud-sdk /usr/local/Caskroom/google-cloud-sdk/latest/google-cloud-sdk && \
    /google-cloud-sdk/bin/gcloud components install alpha beta cloud_sql_proxy cloud-build-local docker-credential-gcr # kubectl

RUN pip3 install --upgrade pip && pip3 install attrs deepdiff ruamel.yaml==0.15.42

# https://kubernetes.io/docs/tasks/tools/install-kubectl/
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/${OS}/${KUBECTL_ARCH}/kubectl && \
    curl -LO https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/${OS}/${KUBECTL_ARCH}/kubectl.sha1 && \
    echo "$(cat kubectl.sha1)  kubectl" > kubectl.sha1sum && \
    sha1sum -c kubectl.sha1sum && \
    rm -f kubectl.sha1sum kubectl.sha1 && \
    mv kubectl /usr/local/bin/kubectl && \
    chmod +x /usr/local/bin/kubectl


ENV PATH /google-cloud-sdk/bin:$PATH
ENV PS1 "\u@\h:\w \$"

ENTRYPOINT []

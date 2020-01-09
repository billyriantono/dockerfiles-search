FROM alpine:latest

ENV OS=linux

# latest stable: curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt
ENV KUBECTL_VERSION=v1.16.3
ENV KUBECTL_ARCH=amd64

# https://cloud.google.com/sdk/docs/quickstart-linux
ENV GCLOUD_VERSION=271.0.0
ENV GCLOUD_SHA256SUM=638ad4e343e46c2812d71ec95601fcfdbda8a3b793264b6fa1b3841e60fc8a9c
ENV GCLOUD_ARCH=x86_64

ENV TF_VERSION=0.12.16
ENV TF_ARCH=amd64

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

RUN curl -O https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_${OS}_${TF_ARCH}.zip && \
    curl -O https://releases.hashicorp.com/terraform/${TF_VERSION}/terraform_${TF_VERSION}_SHA256SUMS && \
    grep terraform_${TF_VERSION}_${OS}_${TF_ARCH}.zip terraform_${TF_VERSION}_SHA256SUMS > terraform_${TF_VERSION}_${OS}_${TF_ARCH}.zip.sha256 && \
    sha256sum -c terraform_${TF_VERSION}_${OS}_${TF_ARCH}.zip.sha256 && \
    unzip terraform_${TF_VERSION}_${OS}_${TF_ARCH}.zip && \
    rm -f terraform_${TF_VERSION}_${OS}_${TF_ARCH}.zip terraform_${TF_VERSION}_${OS}_${TF_ARCH}.zip.sha256 terraform_${TF_VERSION}_SHA256SUMS && \
    mv terraform /usr/local/bin/terraform && \
    chmod +x /usr/local/bin/terraform

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

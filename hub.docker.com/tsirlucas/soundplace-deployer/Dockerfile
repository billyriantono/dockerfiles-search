FROM alpine

WORKDIR app

ENV KUBECTL_VERSION=1.11.0
ENV GCLOUD_SDK_VERSION=208.0.2
ENV DOCKER_VERSION=17.03.0-ce
ENV GOOGLE_APPLICATION_CREDENTIALS=./.google-secrets/gcloud_auth.json

ENV PATH $PATH:/usr/local/gcloud/google-cloud-sdk/bin

# Needed linux tools
RUN apk --no-cache add \
  python \
  py-crcmod \
  curl \
  bash \
  libc6-compat \
  openssh-client \
  git \
  sudo \
  zip \
  unzip

# Gcloud
RUN wget https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${GCLOUD_SDK_VERSION}-linux-x86_64.tar.gz &&\
  mv google-cloud-sdk-${GCLOUD_SDK_VERSION}-linux-x86_64.tar.gz /tmp/google-cloud-sdk.tar.gz &&\
  mkdir -p /usr/local/gcloud &&\
  tar -C /usr/local/gcloud -xvf /tmp/google-cloud-sdk.tar.gz &&\
  /usr/local/gcloud/google-cloud-sdk/install.sh &&\
  gcloud --version

# Kubectl
RUN wget https://storage.googleapis.com/kubernetes-release/release/v${KUBECTL_VERSION}/bin/linux/amd64/kubectl &&\
  chmod +x ./kubectl &&\
  sudo mv ./kubectl /usr/local/bin/kubectl &&\
  kubectl version --short --client

# Docker
RUN curl -L -o /tmp/docker-${DOCKER_VERSION}.tgz https://download.docker.com/linux/static/stable/x86_64/docker-${DOCKER_VERSION}.tgz &&\
    tar -xz -C /tmp -f /tmp/docker-${DOCKER_VERSION}.tgz &&\
    mv /tmp/docker/* /usr/bin

FROM alpine:3.10

# Set timezone to UTC by default
RUN ln -sf /usr/share/zoneinfo/Etc/UTC /etc/localtime

RUN apk update && \
  apk add --no-cache --virtual .build-deps && \
  apk add \
  make \
  openssh \
  git \
  nodejs \
  yarn \
  bash \
  bind-tools \
  curl \
  inotify-tools \
  socat \
  git \
  jq

# Install aws-cli
RUN apk -Uuv add groff less python py-pip
RUN pip install awscli
RUN apk --purge -v del py-pip

# Clean
RUN rm /var/cache/apk/*

# Kubectl
ADD https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/linux/amd64/kubectl /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/kubectl

FROM golang:1.8-alpine
MAINTAINER FindAnyEmail <webmaster@findanyemail.net>

ENV GLIDE_VERSION "0.12.3"
ENV GLIDE_URL "https://github.com/Masterminds/glide/releases/download/v${GLIDE_VERSION}/glide-v${GLIDE_VERSION}-linux-amd64.tar.gz"

ENV GOOGLE_CLOUD_SDK_VERSION "150.0.0"
ENV GOOGLE_CLOUD_SDK_URL "https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-${GOOGLE_CLOUD_SDK_VERSION}-linux-x86_64.tar.gz"

# Install additional system packages
RUN apk --update --no-cache add \
        git \
        tar \
        bash \
        curl \
        docker \
        python \
        openssh-client && \
    go get \
        github.com/jstemmer/go-junit-report

# Install Glide
RUN mkdir -p /opt/glide && \
    curl -sL $GLIDE_URL | tar -xz -C /opt/glide --strip=1 linux-amd64/glide && \
    ln -s /opt/glide/glide /usr/local/bin

# Install Google Cloud SDK
RUN curl -sL $GOOGLE_CLOUD_SDK_URL | tar -zx -C /opt && \
    /opt/google-cloud-sdk/install.sh \
        --quiet \
        --additional-components \
            kubectl \
            docker-credential-gcr
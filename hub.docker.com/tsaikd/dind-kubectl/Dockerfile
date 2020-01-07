FROM docker:dind
RUN apk --no-cache add \
    bash \
    ca-certificates \
    curl \
    jq \
    openssl \
    vim \
    $()
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
    && chmod +x kubectl \
    && mv kubectl /usr/local/bin \
    && $()
RUN curl -sL https://raw.githubusercontent.com/helm/helm/master/scripts/get | bash
CMD bash

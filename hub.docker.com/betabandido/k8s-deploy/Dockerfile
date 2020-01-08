FROM alpine:3.7

RUN apk add --no-cache curl

# Install kubectl
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl

# Install helm
RUN curl -LO https://storage.googleapis.com/kubernetes-helm/helm-v2.9.1-linux-amd64.tar.gz
RUN tar -zxvf helm-v2.9.1-linux-amd64.tar.gz
RUN mv linux-amd64/helm /usr/local/bin/helm

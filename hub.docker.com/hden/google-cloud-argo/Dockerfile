FROM google/cloud-sdk:latest
ARG ARGO_VERSION=2.2.1
ENV ARGO_VERSION=$ARGO_VERSION
RUN curl -sSL -o /usr/local/bin/argo https://github.com/argoproj/argo/releases/download/v${ARGO_VERSION}/argo-linux-amd64 && \
    chmod +x /usr/local/bin/argo
CMD ['argo']

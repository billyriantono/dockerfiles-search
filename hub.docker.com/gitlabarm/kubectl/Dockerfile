# ARGS for entire build
ARG KUBECTL_VERSION="v1.12.10"

FROM debian:stretch-slim
# ARG must be redeclared after each FROM
ARG KUBECTL_VERSION
ARG YQ_VERSION="2.3.0"

# Providing to environment, for easy information gathering.
ENV KUBECTL_VERSION ${KUBECTL_VERSION}

RUN apt-get update \
  && apt-get install -y --no-install-recommends curl ca-certificates libssl1.0.2 openssh-client \
  && curl -LsO https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/arm/kubectl \
  && chmod +x kubectl \
  && mv kubectl /usr/local/bin/kubectl \
  && curl -LsO https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_arm \
  && chmod +x yq_linux_arm \
  && mv yq_linux_arm /usr/local/bin/yq

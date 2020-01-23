FROM ubuntu:18.04

# Metadata
LABEL org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.name="helm-kubectl" \
      org.label-schema.url="https://hub.docker.com/r/dtzar/helm-kubectl/" \
      org.label-schema.vcs-url="https://github.com/dtzar/helm-kubectl" \
      org.label-schema.build-date=$BUILD_DATE

# Note: Latest version of kubectl may be found at:
# https://aur.archlinux.org/packages/kubectl-bin/
ENV KUBE_LATEST_VERSION="v1.13.2"
# Note: Latest version of helm may be found at:
# https://github.com/kubernetes/helm/releases
ENV HELM_VERSION="v2.14.1"
# Latest is curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4
ENV KOPS_VERSION="1.12.2"
ENV HELMFILE_VERSION="v0.79.3"

RUN apt update -y && \
    apt install -y ca-certificates bash git wget curl python3.6 python3-pip jq && \
    update-alternatives --install /usr/bin/python python /usr/bin/python3.6 10

# Kubectl
RUN wget -q https://storage.googleapis.com/kubernetes-release/release/${KUBE_LATEST_VERSION}/bin/linux/amd64/kubectl -O /usr/local/bin/kubectl && \
    chmod +x /usr/local/bin/kubectl

# HELM
RUN wget -q https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz -O - | tar -xzO linux-amd64/helm > /usr/local/bin/helm && \
    chmod +x /usr/local/bin/helm && \
    helm init --client-only && \
    helm repo add jupyterhub https://jupyterhub.github.io/helm-chart/ && \
    helm repo update && \
    helm plugin install https://github.com/databus23/helm-diff --version master

# Kops
RUN curl -Lo kops https://github.com/kubernetes/kops/releases/download/${KOPS_VERSION}/kops-linux-amd64 && \
    chmod +x ./kops && \
    mv ./kops /usr/local/bin/

# Helmfile
RUN curl -Lo helmfile https://github.com/roboll/helmfile/releases/download/${HELMFILE_VERSION}/helmfile_linux_amd64 && \
    chmod +x ./helmfile && \
    mv ./helmfile /usr/local/bin/

# pip
COPY requirements.txt /tmp/requirements.txt
RUN pip3 install -r /tmp/requirements.txt

# commands
ENV PATH="/usr/local/bin/:$PATH"
COPY bin/fetch-secret /usr/local/bin/fetch-secret

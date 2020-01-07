FROM google/cloud-sdk:alpine
ENV TERRAFORM_DOWNLOAD_NAME terraform_0.11.14_linux_amd64.zip
ENV TERRAFORM_DOWNLOAD_URL https://releases.hashicorp.com/terraform/0.11.14/terraform_0.11.14_linux_amd64.zip
ENV HELM_DOWNLOAD_URL https://storage.googleapis.com/kubernetes-helm/helm-v2.14.3-linux-amd64.tar.gz
RUN gcloud components install kubectl --quiet && \
    curl -L ${HELM_DOWNLOAD_URL} | tar -xzv linux-amd64/helm && \
    mv linux-amd64/helm /usr/local/bin/helm && \
    curl -O ${TERRAFORM_DOWNLOAD_URL} && \
    unzip ${TERRAFORM_DOWNLOAD_NAME} && \
    mv terraform /usr/local/bin/terraform && \
    rm ${TERRAFORM_DOWNLOAD_NAME} && \
    curl -Lo skaffold https://storage.googleapis.com/skaffold/releases/v0.35.0/skaffold-linux-amd64 && \
    chmod +x skaffold && \
    mv skaffold /usr/local/bin && \
    curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
ADD . /

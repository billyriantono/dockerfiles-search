FROM centos:7
MAINTAINER Mehedi H <@imehedi on GitHub>

USER root

# Add Amzon Linux extras and few essentials
RUN yum -y install epel-release && \
    yum -y update && \
    yum -y install python2-pip tar gzip wget unzip openssh openssh-clients git && \
    yum -y clean all && \
    pip install --upgrade pip

# Add kops, helm and kubectl
RUN curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64 && \
    chmod +x kops-linux-amd64 && \
    mv kops-linux-amd64 /usr/local/bin/kops && \
    curl https://storage.googleapis.com/kubernetes-helm/helm-v2.11.0-linux-arm64.tar.gz --output helm-v2.11.0-linux-arm64.tar.gz && \
    tar -zxvf helm-v2.11.0-linux-arm64.tar.gz && \
    chmod +x linux-arm64/helm && \
    mv linux-arm64/helm /usr/local/bin/helm && \
    chmod +x linux-arm64/tiller && \
    mv linux-arm64/tiller /usr/local/bin/tiller && \
    rm -rf helm-v2.11.0-linux-arm64.tar.gz linux-arm64 && \
    curl https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/linux/amd64/kubectl --output kubectl && \
    chmod +x kubectl && \
    mv kubectl /usr/local/bin/kubectl

# Add terraform
RUN wget --quiet https://releases.hashicorp.com/terraform/0.11.3/terraform_0.11.3_linux_amd64.zip \
  && unzip terraform_0.11.3_linux_amd64.zip \
  && mv terraform /usr/local/bin/terraform \
  && rm terraform_0.11.3_linux_amd64.zip

# Add GCP SDk
RUN mkdir -p /etc/yum.repos.d/
COPY repo-file/* /etc/yum.repos.d/

RUN yum -y update && \
    yum -y install google-cloud-sdk \
    google-cloud-sdk-app-engine-python \
    google-cloud-sdk-app-engine-python-extras \
    google-cloud-sdk-app-engine-java \
    google-cloud-sdk-app-engine-go \
    google-cloud-sdk-bigtable-emulator \
    google-cloud-sdk-datalab \
    google-cloud-sdk-datastore-emulator \
    google-cloud-sdk-cbt \
    google-cloud-sdk-cloud-build-local \
    google-cloud-sdk-pubsub-emulator && \
    yum -y clean all

# Copy init for bootstrap
COPY docker-entrypoint.sh /usr/local/bin/


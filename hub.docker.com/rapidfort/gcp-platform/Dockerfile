FROM google/cloud-sdk:latest
ENV HELM_VERSION="v3.0.0" \
    GOLANG_VERSION="1.13.4" \
    TERRAFORM_VERSION="0.12.17" \
    GOROOT="/usr/local/go" \
    GOBIN="/usr/local/go/bin" \
    GOPATH="/opt" \
    PATH="$PATH:$GOBIN:$GOPATH/bin:."

RUN apt update -y && apt install -y wget unzip jq ansible && wget -q https://get.helm.sh/helm-${HELM_VERSION}-linux-amd64.tar.gz -O - | tar -xzO linux-amd64/helm > /usr/local/bin/helm && chmod +x /usr/local/bin/helm \
    && wget -q https://dl.google.com/go/go${GOLANG_VERSION}.linux-amd64.tar.gz && tar xf go${GOLANG_VERSION}.linux-amd64.tar.gz -C /usr/local && rm go${GOLANG_VERSION}.linux-amd64.tar.gz \
    && wget -q https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
    && unzip -o terraform_${TERRAFORM_VERSION}_linux_amd64.zip -d /usr/local/bin && chmod 755 /usr/local/bin/terraform && rm terraform_${TERRAFORM_VERSION}_linux_amd64.zip \
    && rm -rf /var/lib/apt/lists/*

FROM alpine:3.10

RUN set -x && apk add --no-cache curl python3 bash gettext && \
    pip3 install awscli && \
    curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.14.10/bin/linux/amd64/kubectl && \
    chmod +x ./kubectl && \
    mv ./kubectl /usr/local/bin/kubectl && \
    curl -LO https://storage.googleapis.com/kubernetes-helm/helm-v2.16.1-linux-amd64.tar.gz && \
    tar -zxvf helm-v2.16.1-linux-amd64.tar.gz && \
    mv linux-amd64/helm /usr/local/bin/helm && \
    rm -rf helm-v2.16.1-linux-amd64.tar.gz && \
    curl -LO https://amazon-eks.s3-us-west-2.amazonaws.com/1.14.6/2019-08-22/bin/linux/amd64/aws-iam-authenticator && \
    chmod +x ./aws-iam-authenticator && \
    mv aws-iam-authenticator /usr/local/bin/aws-iam-authenticator && \
    aws --version && \
    kubectl version --client && \
    helm version --client && \
    aws-iam-authenticator version

CMD ["/bin/bash"]

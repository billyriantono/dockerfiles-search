FROM golang:alpine
ENV TERRAFORM_VERSION=0.10.0
ENV TF_DEV=true
ENV TF_RELEASE=true

RUN apk add --update git bash openssh make ca-certificates openssl python

WORKDIR $GOPATH/src/github.com/hashicorp/terraform
RUN git clone https://github.com/hashicorp/terraform.git ./ && \
    git checkout v${TERRAFORM_VERSION} && \
    /bin/bash scripts/build.sh
    
RUN wget https://dl.google.com/dl/cloudsdk/release/google-cloud-sdk.tar.gz \
    && tar zxvf google-cloud-sdk.tar.gz && ./google-cloud-sdk/install.sh --usage-reporting=false --path-update=true \
    && google-cloud-sdk/bin/gcloud --quiet components update

WORKDIR $GOPATH
ENTRYPOINT ["terraform"]

FROM dfdsdk/terragrunt-runner:0.3

ENV BASE_URL="https://storage.googleapis.com/kubernetes-helm"
ENV TAR_FILE="helm-v2.12.1-linux-amd64.tar.gz"

RUN apk add --update --no-cache python3 curl ca-certificates
RUN python3 -m pip install --upgrade pip && \
    pip3 install pipenv awscli

# Install kubectl & AWS Authenticator
RUN curl -L https://storage.googleapis.com/kubernetes-release/release/v1.12.0/bin/linux/amd64/kubectl -o ~/kubectl && \
    chmod +x ~/kubectl && \
    mv ~/kubectl /usr/local/bin/ && \
    curl -L https://amazon-eks.s3-us-west-2.amazonaws.com/1.10.3/2018-07-26/bin/linux/amd64/aws-iam-authenticator -o ~/aws-iam-authenticator && \
    chmod +x ~/aws-iam-authenticator && \
    mv ~/aws-iam-authenticator /usr/local/bin/

RUN curl -L https://github.com/weaveworks/flux/releases/download/1.8.2/fluxctl_linux_amd64 -o ~/fluxctl && \
    chmod +x ~/fluxctl && \
    mv ~/fluxctl /usr/local/bin/

# Install Helm
# Snateched from https://github.com/alpine-docker/helm/blob/master/Dockerfile
RUN curl -L ${BASE_URL}/${TAR_FILE} |tar xvz && \
    mv linux-amd64/helm /usr/bin/helm && \
    chmod +x /usr/bin/helm && \
    rm -rf linux-amd64 && \
    rm -f /var/cache/apk/*
    
COPY ./src ./src

RUN cd ./src && pipenv install --system --deploy --ignore-pipfile

ENTRYPOINT ["/bin/terragrunt"]
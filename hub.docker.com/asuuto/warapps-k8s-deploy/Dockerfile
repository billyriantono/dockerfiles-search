FROM asuuto/ci-build:latest
LABEL maintainer="Nate Wilken <wilken@asu.edu>"

ENV KUBE_VERSION=v1.14.0
ENV HELM_VERSION=v2.13.1

WORKDIR /bin
RUN curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBE_VERSION}/bin/linux/amd64/kubectl -o kubectl \
 && chmod +x kubectl \
 && curl -L https://storage.googleapis.com/kubernetes-helm/helm-${HELM_VERSION}-linux-amd64.tar.gz -o /tmp/helm.tgz \
 && tar xf /tmp/helm.tgz --strip-components=1 linux-amd64/helm \
 && rm /tmp/helm.tgz \
 && chmod +x helm \
 && curl -o /tmp/aws-iam-authenticator https://amazon-eks.s3-us-west-2.amazonaws.com/1.12.7/2019-03-27/bin/linux/amd64/aws-iam-authenticator \
 && chmod +x /tmp/aws-iam-authenticator

RUN apk update \
 && apk add --no-cache gettext py-pip \
 && pip install --no-cache-dir --upgrade pip \
 && pip install --no-cache-dir python-gilt \
 && rm -rf /root/.cache

WORKDIR /deploy
COPY gilt.yml .
RUN chown -R 1000:1000 .

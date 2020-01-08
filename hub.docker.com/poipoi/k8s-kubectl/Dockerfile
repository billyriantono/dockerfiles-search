FROM alpine:3.8

ENV KUBECTL_VERSION="v1.13.1"
ENV AWS_IAM_AUTHENTICATOR="1.10.3"

RUN apk -v --update add \
     ca-certificates \
     python3 \
     less \
     mailcap \
     curl \
     bash \
     bash-doc \
     bash-completion
RUN  curl -L https://storage.googleapis.com/kubernetes-release/release/${KUBECTL_VERSION}/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl && \
     curl -L https://amazon-eks.s3-us-west-2.amazonaws.com/${AWS_IAM_AUTHENTICATOR}/2018-07-26/bin/linux/amd64/aws-iam-authenticator -o /usr/local/bin/aws-iam-authenticator && \
     chmod +x /usr/local/bin/aws-iam-authenticator && \
     chmod +x /usr/local/bin/kubectl
RUN  python3 -m ensurepip && \
     rm -r /usr/lib/python*/ensurepip && \
     pip3 install --upgrade pip setuptools && \
     pip3 install --upgrade awscli==1.16.68 python-magic && \
     if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi && \
     if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi
RUN  rm /var/cache/apk/*

VOLUME /root/.aws
VOLUME /root/.kube

VOLUME /work
WORKDIR /work

FROM alpine:latest
MAINTAINER william.mcmath+probablyspam@gmail.com

RUN apk add curl py-pip \
	&& pip install awscli \
    && curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.14.7/bin/linux/amd64/kubectl \
    && chmod +x ./kubectl \
    && mv ./kubectl /usr/local/bin/kubectl \
    && curl -o aws-iam-authenticator https://amazon-eks.s3-us-west-2.amazonaws.com/1.14.6/2019-08-22/bin/linux/amd64/aws-iam-authenticator \
    && chmod +x ./aws-iam-authenticator \
    && mv ./aws-iam-authenticator /usr/local/bin/aws-iam-authenticator \
    && mkdir /.kube \
    && mkdir /.aws

USER 1111
ENTRYPOINT [ "kubectl" ]
CMD [ "--help" ]

FROM alpine:3.10

ENV PYTHON_VERSION=3.7.3-r0 \
    PIP_VERSION=19.1.1 \
    AWSCLI_VERSION=1.16.199 \
		KUBECTL_VERSION=v1.15.0

# Install python3
RUN apk add --no-cache python3=$PYTHON_VERSION curl && \
    if [ ! -e /usr/bin/python ]; then ln -sf python3 /usr/bin/python ; fi

# Install pip, awscli
RUN python3 -m ensurepip && \
    rm -r /usr/lib/python*/ensurepip && \
    pip3 install --no-cache pip==$PIP_VERSION awscli==$AWSCLI_VERSION && \
    if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi

# Install kubectl
RUN curl -s -o /usr/local/bin/kubectl \
    -L https://storage.googleapis.com/kubernetes-release/release/$KUBECTL_VERSION/bin/linux/amd64/kubectl && \
	  chmod +x /usr/local/bin/kubectl

# Install aws-iam-authenticator
RUN curl -s -o /usr/local/bin/aws-iam-authenticator \
    -L https://amazon-eks.s3-us-west-2.amazonaws.com/1.13.7/2019-06-11/bin/linux/amd64/aws-iam-authenticator && \
    chmod +x /usr/local/bin/aws-iam-authenticator

# Cleanup
RUN apk -v --purge del curl

ENTRYPOINT ["/bin/sh","-c"]
CMD [""]
WORKDIR /tmp
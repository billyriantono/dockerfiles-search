ARG BASE_IMAGE
FROM docker:${BASE_IMAGE:-stable-dind}

ARG PACKER_VERSION
ARG PACKER_SHA256SUM

ENV PACKER_VERSION=${PACKER_VERSION:-1.4.5}
ENV PACKER_SHA256SUM=${PACKER_SHA256SUM:-b4dc37877a0fd00fc72ebda98977c2133be9ba6b26bcdd13b1b14a369e508948}

ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip ./
ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_SHA256SUMS ./

RUN apk add --update git bash wget openssl && \
    sed -i '/.*linux_amd64.zip/!d' packer_${PACKER_VERSION}_SHA256SUMS && \
    sha256sum -cs packer_${PACKER_VERSION}_SHA256SUMS && \
    unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /bin && \
    rm -f packer_${PACKER_VERSION}_linux_amd64.zip

ENTRYPOINT ["/bin/packer"]

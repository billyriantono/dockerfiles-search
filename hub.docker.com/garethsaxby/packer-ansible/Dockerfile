FROM library/alpine:3.8

ENV PACKER_VERSION=1.2.5
ENV ANSIBLE_VERSION=2.6.1

# Installing Packer
RUN apk add --no-cache wget && \
wget -nv https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip && \
wget -nv https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_SHA256SUMS && \
sed -i '/.*linux_amd64.zip/!d' packer_${PACKER_VERSION}_SHA256SUMS && \
sha256sum -cs packer_${PACKER_VERSION}_SHA256SUMS && \
unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /bin && \
rm -f packer_${PACKER_VERSION}_linux_amd64.zip && \
apk del --no-cache wget

# Installing Ansible
RUN apk add --no-cache python2 py2-pip openssl ca-certificates python2-dev libffi-dev openssl-dev build-base && \
pip install ansible==${ANSIBLE_VERSION} && \
apk del --no-cache python2-dev libffi-dev openssl-dev build-base

ENTRYPOINT ["/bin/packer"]
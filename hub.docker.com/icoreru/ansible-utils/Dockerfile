# Dockerfile for build ansible image with as few additional software (Ansible and requirements for modules).
FROM alpine:3.8
ENV ANSIBLE_VER="2.7.4"
ENV SHADE_VER="1.30.0"
ENV OPENSTACKSDK_VER="0.22.0"
RUN echo "===> Installing software..." && \
    apk --update add sudo openssl ca-certificates make openssh-client linux-headers py-netaddr && \
    \
    echo "===> Adding Python runtime..." && \
    apk --update add python py-pip && \
    apk --update add --virtual build-dependencies \
    python-dev libffi-dev openssl-dev build-base  && \
    pip install --upgrade pip cffi && \
    \
    echo "===> Installing Ansible..." && \
    pip install "ansible==${ANSIBLE_VER}" && \
    \
    echo "===> Installing Shade..." && \
    pip install "shade==${SHADE_VER}" && \
    \
    echo "===> Installing OpenstackSDK..." && \
    pip install "openstacksdk==${OPENSTACKSDK_VER}" && \
    \
    echo "===> Cleaning..." && \
    apk del build-dependencies linux-headers && \
    rm -rf /var/cache/apk/* && \
    rm -rf /tmp
WORKDIR /deploy/ansible
ENTRYPOINT [ "make" ]

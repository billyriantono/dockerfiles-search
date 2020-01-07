FROM gliderlabs/alpine:3.2

MAINTAINER Arthur Tsang <amaryllis.arthur@gmail.com>

ENV ANSIBLE_VERSION 2.0.0.2
ENV ANSIBLE_CONFIG /ansible.cfg

RUN apk add --update python py-pip py-crypto openssh-client sshpass libtool python-dev automake autoconf alpine-sdk 

RUN \
    pip install --upgrade pip && \
    pip install --upgrade six && \
    pip install pyjq && \
    pip install ansible==${ANSIBLE_VERSION} 

RUN apk del libtool python-dev automake autoconf alpine-sdk && \
    rm -rf /var/cache/apk/*

ADD ansible.cfg /ansible.cfg
ADD run.sh /run.sh

RUN chmod 755 /run.sh

ENTRYPOINT ["/run.sh"]

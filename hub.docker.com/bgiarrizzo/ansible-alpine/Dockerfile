# 12-09-2019

FROM python:alpine

RUN apk update \
    apk add sudo && \
    apk add openssl ca-certificates openssh-client git sshpass openssh-client rsync curl && \
    apk add --virtual build-dependencies python-dev libffi-dev openssl-dev build-base && \
    pip install --upgrade pip cffi && \
    pip install ansible ansible-lint pycrypto pywinrm docker && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk/*

WORKDIR /ansible/

VOLUME /ansible/ /root/.ssh/

CMD [ "ansible-playbook", "--version" ]

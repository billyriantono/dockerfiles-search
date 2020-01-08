ARG ALPINE_VERSION
FROM alpine:${ALPINE_VERSION:-latest}

RUN set -x && \
    apk add --no-cache --virtual .build-deps gcc build-base \
    linux-headers ca-certificates python3-dev libffi-dev libressl-dev && \
    apk add --no-cache --virtual .required \
    python3 py3-pip openssh git && \
    pip3 install --upgrade pip && \
    pip3 install ansible argcomplete && \
    apk del .build-deps && rm -rf /var/cache/apk/*

RUN set -x && \
    mkdir -p /ansible/hosts /ansible/playbooks /ansible/roles && \
    printf "[local]\nlocalhost ansible_connection=local" > /ansible/hosts/all && \
    addgroup -S ansible && adduser -S ansible -G ansible && \
    chown -R ansible:ansible /ansible

ENV ANSIBLE_INVENTORY=/ansible/hosts \
    ANSIBLE_PLAYBOOK_DIR=/ansible/playbooks \
    ANSIBLE_ROLES_PATH=/ansible/roles \
    ANSIBLE_GATHERING=smart \
    ANSIBLE_HOST_KEY_CHECKING=false \
    ANSIBLE_RETRY_FILES_ENABLED=false \
    ANSIBLE_SSH_PIPELINING=true \
    ANSIBLE_PYTHON_INTERPRETER=/usr/bin/python3

WORKDIR /ansible
USER ansible

ENTRYPOINT ["/usr/bin/env"]
CMD ["ansible-playbook", "--version"]

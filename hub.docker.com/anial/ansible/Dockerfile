ARG ALPINE_VERSION=3.10
FROM alpine:${ALPINE_VERSION}

ARG ANSIBLE_VERSION="2.8.5"

#
# Install requirenments
#
RUN set -ex \
    && apk add --no-cache --update \
            python3 ca-certificates openssh-client sshpass bash su-exec rsync \
    && apk add --no-cache --update --virtual \
           .build-deps python3-dev build-base libffi-dev openssl-dev \
    \
    && pip3 install --no-cache --upgrade \
            pip \
    && pip3 install --no-cache --upgrade \
            setuptools ansible==${ANSIBLE_VERSION} \
    \
    && apk del --no-cache --purge .build-deps \
    && rm -rf /var/cache/apk/* /root/.cache \
    \
    && ln -s /usr/bin/python3 /usr/bin/python

#
# Create user ansible
#
RUN set -ex \
    && mkdir -p /etc/ansible/ \
    && /bin/echo -e "[local]\nlocalhost ansible_connection=local" > /etc/ansible/hosts ;\
    \
    adduser -s /bin/bash -u 1000 -D -h /ansible ansible \
    && mkdir -p /ansible/.ssh \
    && ssh-keygen -q -t ed25519 -N '' -f /ansible/.ssh/id_ed25519 \
    && echo "Host *" > /ansible/.ssh/config && echo " StrictHostKeyChecking no" >> /ansible/.ssh/config


COPY ./docker-entrypoint.sh /
ENTRYPOINT ["/docker-entrypoint.sh"]

WORKDIR /ansible/playbooks

CMD ["ansbile" "--version"]

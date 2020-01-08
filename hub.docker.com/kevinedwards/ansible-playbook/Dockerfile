FROM python:alpine

LABEL maintainer="Kevin Edwards <kedwards@kevinedwards.ca>"

ENV BUILD_DEPS "libffi-dev openssl-dev build-base"

ENV PACKAGES "openssl sshpass rsync openssh-client ca-certificates"
 
RUN apk update && \
    apk upgrade && \
    apk add --no-cache --virtual=build-dependencies ${BUILD_DEPS} && \
    apk add --no-cache ${PACKAGES} && \
    pip3 install --upgrade pip cffi  && \
    pip3 install --upgrade pywinrm && \
    pip3 install ansible==2.9.1 && \
    pip3 install --upgrade pywinrm && \
    apk del build-dependencies && \
    rm -rf /var/cache/apk/* && \
    mkdir -p /etc/ansible/playbooks && \
    echo '[local]' > /etc/ansible/hosts && \
    echo 'localhost ansible_connection=local' >> /etc/ansible/hosts

ENV ANSIBLE_GATHERING smart
ENV ANSIBLE_HOST_KEY_CHECKING false
ENV ANSIBLE_RETRY_FILES_ENABLED false
ENV ANSIBLE_ROLES_PATH /ansible/playbooks/roles
ENV ANSIBLE_SSH_PIPELINING True
ENV PYTHONPATH /ansible/lib
ENV PATH /ansible/bin:$PATH
ENV ANSIBLE_LIBRARY /ansible/library

WORKDIR /ansible/playbooks

VOLUME [ "/ansible/playbooks" ]

ENTRYPOINT ["ansible-playbook"]

CMD ["--version" ]
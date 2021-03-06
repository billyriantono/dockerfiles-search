# Dockerfile for building Ansible image for Alpine 3, with as few additional software as possible.
#
# Version  2.0
#

FROM alpine:3.10

RUN echo -e "\nInstalling sudo to emulate normal OS behavior...\n"  && \
    apk --update add sudo                                           && \
    \
    \
    echo -e "\nAdding Python runtime...\n"  && \
    apk --update add python3 py3-pip openssl ca-certificates    && \
    apk --update add --virtual build-dependencies \
                python3-dev libffi-dev openssl-dev build-base   && \
    pip3 install --upgrade pip                                  && \
    \
    \
    echo -e "\nInstalling Ansible...\n"        && \
    pip install ansible jmespath               && \
    \
    \
    echo -e "\nInstalling handy tools (not absolutely required)...\n"  && \
    pip install --upgrade pycrypto pywinrm         && \
    apk --update add sshpass openssh-client rsync  && \
    \
    \
    echo -e "\nRemoving package list...\n"  && \
    apk del build-dependencies              && \
    rm -rf /var/cache/apk/*                 && \
    \
    \
    echo -e "\nAdding hosts for convenience...\n"  && \
    mkdir -p /etc/ansible                          && \
    echo 'localhost' > /etc/ansible/hosts

# default command: display Ansible version
CMD [ "ansible-playbook", "--version" ]

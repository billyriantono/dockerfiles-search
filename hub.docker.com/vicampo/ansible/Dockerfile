FROM alpine:3.6

MAINTAINER Manuel Schmidt <manuel.schmidt@vicampo.de>

RUN echo "===> Installing sudo to emulate normal OS behavior..." && \
  apk --update add sudo && \

  echo "===> Adding Python runtime..." && \
  apk --update add python py-pip openssl ca-certificates && \
  apk --update add --virtual build-dependencies \
  python-dev libffi-dev openssl-dev build-base && \
  pip install --upgrade pip cffi && \

  echo "===> Installing Ansible..." && \
  pip install ansible==2.4.2 && \

  echo "===> Installing handy tools (not absolutely required)..." && \
  pip install --upgrade pywinrm && \
  apk --update add sshpass openssh-client rsync && \

  echo "===> Removing package list..." && \
  apk del build-dependencies && \
  rm -rf /var/cache/apk/*
CMD [ "ansible-playbook", "--version" ]

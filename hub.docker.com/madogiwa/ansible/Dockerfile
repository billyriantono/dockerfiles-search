
FROM python:3
LABEL maintainer="Hidenori Sugiyama <madogiwa@gmail.com>"

RUN \
  pip install --no-cache-dir ansible

RUN \
  groupadd -g 1000 ansible && \
  useradd -g ansible -u 1000 -m ansible

COPY ansible.cfg /etc/ansible/ansible.cfg

USER ansible
WORKDIR /ansible

VOLUME [ "/home/ansible/.ssh", "/ansible" ]

ENTRYPOINT [ "ansible" ]


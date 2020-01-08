FROM python:3.7.2-slim

RUN apt-get update && apt-get install -y \
    openssh-client \
    && rm -rf /var/lib/apt/lists/*

RUN pip install ansible

COPY ["ansible.cfg", "/etc/ansible/ansible.cfg"]

ARG USER_ID=1000
RUN mkdir /ssh-key && chown "$USER_ID":"$USER_ID" /ssh-key

RUN groupadd --gid "$USER_ID" appuser \
    && useradd --uid "$USER_ID" --gid "$USER_ID" --create-home appuser

USER appuser

RUN yes y | ssh-keygen -t rsa -b 4096 -N '' -C '' -m 'PEM' -f /ssh-key/ansible.pem >> /dev/null

WORKDIR /ansible
VOLUME /ansible

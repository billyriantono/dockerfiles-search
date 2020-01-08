FROM alpine:latest
MAINTAINER biotecs
ENV ANSIBLE_SSH_ARGS="-i /etc/ansible/keys/ansible_key"
ENV ANSIBLE_SSH_ARGS="-o UserKnownHostsFile=/etc/ansible/keys/known_hosts $ANSIBLE_SSH_ARGS"
RUN apk --no-cache add git py2-pip py-paramiko py-crypto perl rsync openssh sshpass openssl curl && rm -rf /var/cache/apk/*
RUN pip install ansible
RUN mkdir -p /etc/ansible
RUN echo "[local]" > /etc/ansible/hosts; echo "localhost ansible_ssh_host=172.17.0.1" >> /etc/ansible/hosts
WORKDIR /etc/ansible
CMD ["/bin/sh"]

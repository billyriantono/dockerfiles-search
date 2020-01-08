FROM alpine:3.9

RUN apk add --no-cache python3 curl openssh-client alpine-sdk python3-dev libffi-dev openssl-dev && \
  pip3 install ansible && \
  apk del alpine-sdk alpine-sdk python3-dev libffi-dev openssl-dev

RUN mkdir /root/.ssh/ && echo -e 'StrictHostKeyChecking no\n' > /root/.ssh/config && chmod 0600 /root/.ssh/config && \
  touch /root/.ssh/id_songsterr_deploy && chmod 0600 /root/.ssh/id_songsterr_deploy && \
  mkdir /etc/ansible/

ADD ansible.cfg /etc/ansible/ansible.cfg
ADD script.sh /bin/
ADD docker-gc-playbook.yml /etc/ansible/
RUN chmod +x /bin/script.sh && chmod 0600 /etc/ansible/ansible.cfg
ENTRYPOINT /bin/script.sh

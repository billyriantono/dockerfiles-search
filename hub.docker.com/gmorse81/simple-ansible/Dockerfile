FROM ubuntu:xenial

RUN apt-get update && apt-get install -y python2.7 curl \
  && curl -O https://bootstrap.pypa.io/get-pip.py \
  && python2.7 get-pip.py \
  && pip install ansible

RUN mkdir /var/ansible_proj_root

WORKDIR /var/ansible_proj_root

ENTRYPOINT ["ansible-playbook"]
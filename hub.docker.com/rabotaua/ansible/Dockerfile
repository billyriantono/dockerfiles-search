FROM python:2

WORKDIR /code

RUN  apt-get update && apt-get install sshpass -y
RUN  pip install ansible==2.6.2
RUN  pip install jmespath

# https://docs.ansible.com/ansible/latest/reference_appendices/config.html
ENV ANSIBLE_HOST_KEY_CHECKING false

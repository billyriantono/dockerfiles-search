FROM williamyeh/ansible:ubuntu14.04
MAINTAINER luisperlazaro@gmail.com

COPY ansible/role_playbook.yml /tmp/ansible/role_playbook.yml
COPY ansible/roles /tmp/ansible/roles

WORKDIR /tmp/ansible

RUN ansible-playbook -c local role_playbook.yml -e role=java
RUN ansible-playbook -c local role_playbook.yml -e role=gradle

WORKDIR /

ENTRYPOINT ["/bin/bash", "--login"]


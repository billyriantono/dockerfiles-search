FROM luisperlaz/jython
MAINTAINER luisperlazaro@gmail.com

COPY ansible/role_playbook.yml /tmp/ansible/role_playbook.yml
COPY ansible/roles /tmp/ansible/roles

ENTRYPOINT ["/bin/bash", "--login"]

RUN ansible-playbook -c local /tmp/ansible/role_playbook.yml -e role=django
RUN ansible-playbook -c local /tmp/ansible/role_playbook.yml -e role=karma


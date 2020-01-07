FROM luisperlaz/djangojythondev
MAINTAINER luisperlazaro@gmail.com

COPY ansible/role_playbook.yml /tmp/ansible/role_playbook.yml

COPY ansible/roles/django_pages_cms /tmp/ansible/roles/django_pages_cms
RUN ansible-playbook -c local /tmp/ansible/role_playbook.yml -e role=django_pages_cms

ENTRYPOINT ["/bin/bash", "--login"]


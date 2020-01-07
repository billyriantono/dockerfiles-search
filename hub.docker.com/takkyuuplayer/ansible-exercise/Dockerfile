FROM geerlingguy/docker-debian9-ansible

COPY ansible.cfg hosts.ini site.yml roles /tmp/provisioner/

WORKDIR /tmp/provisioner

RUN ansible-playbook -i hosts.ini site.yml
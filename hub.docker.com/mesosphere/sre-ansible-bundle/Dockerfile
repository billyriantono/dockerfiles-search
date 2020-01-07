FROM mesosphere/dcos-ansible-bundle:latest
RUN mv dcos_playbook.yml dcos_ansible_bundle.yml
COPY ./docker/playbook.yml /dcos_playbook.yml
COPY ./ansible/roles/Mesosphere.Spec /roles/Mesosphere.Spec
COPY ./ansible/roles/Mesosphere.Spec.Logging /roles/Mesosphere.Spec.Logging
COPY ./ansible/ansible.cfg /ansible.cfg
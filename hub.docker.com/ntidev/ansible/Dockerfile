FROM ubuntu:latest

RUN apt-get update && apt-get install software-properties-common -y && apt-add-repository --yes --update ppa:ansible/ansible && apt-get install ansible -y

RUN touch "/var/log/ansible.log"

ENTRYPOINT ["/usr/bin/tail", "-f", "/var/log/ansible.log"]

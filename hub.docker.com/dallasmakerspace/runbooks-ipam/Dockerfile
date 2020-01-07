FROM ansible/ansible:latest
LABEL maintainer=denzuko@dallasmakerspace.org
COPY . /src
WORKDIR /src
RUN ansible-playbooks playbook.yml

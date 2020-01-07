FROM ubuntu:trusty
MAINTAINER Igor Loboda

ENV TERM=xterm-256color

#Install Ansible
RUN apt-get update -qy && \
    apt-get install -qy software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update -qy && \
    apt-get install -qy ansible
#COPY playbook
COPY ansible /ansible

# Add volume for Ansible playbook
VOLUME /ansible
WORKDIR /ansible

ENTRYPOINT ["ansible-playbook"]
# The playbook to run by default
CMD ["site.yml"]

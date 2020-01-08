FROM ubuntu:trusty
MAINTAINER Alejandro Villamarin <favm@email.com>

# Suppress dpkg errors
ENV TERM=xterm-256color

# Set mirrors to CZ
RUN sed -i "s/https:\/\/archive./https:\/\/cz.archive./g" /etc/apt/sources.list

# Install Ansible
RUN apt-get update -qy && \
    apt-get install -qy software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update -qy && \
    apt-get install -qy ansible

# Copy playbooks
COPY ansible /ansible

# Create volume for Ansible playbooks
VOLUME /ansible
WORKDIR /ansible

# Entrypoint
ENTRYPOINT ["ansible-playbook"]
CMD ["site.yml"]
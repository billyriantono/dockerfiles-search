FROM ubuntu:trusty
MAINTAINER Prasant Kumar <publicapi@live.com>

# Prevent dpkg errors
ENV TERM=xterm-256color

# Set mirrors to IN
RUN sed -i "s/http:\/\/archive./http:\/\/in.archive./g" /etc/apt/sources.list

# Install Ansible
RUN apt-get update -qy && \
    apt-get install -qy software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update -qy && \
    apt-get install -qy ansible

# Copy baked in playbooks
COPY ansible /ansible

# Add volume for Ansible playbooks
VOLUME /ansible
WORKDIR /ansible

# Entrypoint
ENTRYPOINT ["ansible-playbook"]
CMD ["site.yml"]

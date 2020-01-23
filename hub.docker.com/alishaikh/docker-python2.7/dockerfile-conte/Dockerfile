FROM ubuntu:trusty
MAINTAINER Aliaksei Kiryanau <aliaksei.kiryanau1@gmail.com>

# Prevent dpkg errors
ENV TERM=xterm-256color

# Set mirrors to BY
RUN sed -i "s/http:\/\/archive./http:\/\/by.archive./g" /etc/apt/sources.list

# Install Ansible
RUN apt-get update -qy && \
	apt-get install -qy software-properties-common && \
	apt-add-repository ppa:ansible/ansible-1.9 && \
	apt-get update -qy && \
	apt-get install -qy ansible

# Copy backed in playbooks
COPY ansible /ansible

# Add volume for Ansible playbooks
VOLUME /ansible
WORKDIR /ansible

# Entrypoint
ENTRYPOINT ["ansible-playbook"]
CMD ["probe.yml"]
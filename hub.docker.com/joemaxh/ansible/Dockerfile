FROM ubuntu:trusty
MAINTAINER Joseph Huhman <joemaxh@gmail.com>

#Prevent dpkg errors
ENV TERM=xterm-256color

# Set mirrors (not doing this step)

#Install Ansible
RUN apt-get update -qy && \
	apt-get install -qy software-properties-common && \
	apt-add-repository -y ppa:ansible/ansible && \
	apt-get update -qy && \
	apt-get install -qy ansible

# Copy baked in playbook
COPY ansible /ansible

# Add volume for Ansible playbooks
VOLUME /ansible
WORKDIR /ansible

# Entrypoint
ENTRYPOINT ["ansible-playbook"]
CMD ["site.yml"]
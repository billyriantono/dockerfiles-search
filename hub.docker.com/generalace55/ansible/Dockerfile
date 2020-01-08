FROM ubuntu:trusty
MAINTAINER Josh Hannaford <Joshua.Hannaford@gmail.com>

# Prevent dpkg errors
ENV TERM=xterm-256color

# Install Ansible
RUN apt-get update -qy && \
    apt-get install -qy software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update -qy && \
    apt-get install -qy ansible

# Copy baked ansible playbook
COPY ansible /ansible

# Add a volume for the Ansible playbook
VOLUME /ansible
WORKDIR /ansible

# Entrypoint
ENTRYPOINT ["ansible-playbook"]
CMD ["site.yml"]
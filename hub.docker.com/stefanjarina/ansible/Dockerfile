FROM ubuntu:trusty
LABEL LABEL maintainer="Stefan Jarina <stefan@jarina.cz>"

# Prevent dpkg errors
ENV DEBIAN_FRONTEND noninteractive
ENV TERM=xterm-256color

# Set mirrors to CZ. One of these might be faster
# In case CVUT doesn't work properly please replace it with official cz.archive.ubuntu.com
RUN sed -i "s/http:\/\/archive./http:\/\/cz.archive./g" /etc/apt/sources.list
# RUN sed -i "s/http:\/\/archive.ubuntu.com/http:\/\/ftp.cvut.cz/g" /etc/apt/sources.list

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
ENTRYPOINT [ "ansible-playbook" ]
CMD ["site.yml"]
FROM ubuntu:trusty
MAINTAINER Tim Kelley <timothy.kelley@ngc.com>

#prevent dpkg errors
ENV TERM=xterm-256color

#Install Ansible
RUN apt-get update -qy && \
    apt-get install -qy software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update -qy && \
    apt-get install -qy ansible

# Copy baked in playbooks
COPY ansible /ansible
    
# Add volume for ansible playbooks
VOLUME /ansible
WORKDIR /ansible
    
# Entrypoint
ENTRYPOINT ["ansible-playbook"]
CMD ["site.yml"]    

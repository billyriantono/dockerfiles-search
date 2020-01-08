FROM ubuntu:trusty
LABEL Smilen Stoychev <stoychevs10@gmail.com>

# prevent dpkg errors
ENV TERM=xterm-256color

RUN sed -i "s/http:\/\/archive./http:\/\/nz.archive./g" /etc/apt/sources.list

# Install Ansible
RUN apt-get update -qy && \
    apt-get install -qy software-properties-common && \
    apt-add-repository -y ppa:ansible/ansible && \
    apt-get update -qy && \
    apt-get install -qy ansible

COPY ansible /ansible

# Add volume for Ansible plbooks
VOLUME /ansible
WORKDIR /ansible

ENTRYPOINT [ "ansible-playbook" ]
CMD ["site.yml"]
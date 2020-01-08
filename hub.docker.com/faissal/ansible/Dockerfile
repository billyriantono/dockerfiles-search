FROM ubuntu:trusty
MAINTAINER faissal bibelghach <glfaissal@gmail.com>

# Prevent dpkg errors
ENV TERM=xterm-256color

# Install Ansible
# RUN apt-get update -qy && \
#     apt-get install -qy software-properties-common && \
#     apt-add-repository -y ppa:ansible/ansible && \
#     apt-get update -qy && \
#     apt-get install -qy ansible


COPY ./wait-for-it.sh /usr/local/bin/wait-for-it.sh
COPY ./wait-command.sh /usr/local/bin/wait-command.sh
RUN chmod +x /usr/local/bin/wait-for-it.sh
RUN chmod +x /usr/local/bin/wait-command.sh


# Copy baked in playbooks
# COPY docker/ansible/ansible /ansible

# Add volume for Ansible playbooks
# VOLUME /ansible
# WORKDIR /ansible

# Entrypoint
#ENTRYPOINT ["ansible-playbook"]
ENTRYPOINT ["wait-command.sh"]

#CMD ["site.yml"]
#CMD ["prob.yml"]
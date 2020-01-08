FROM lol233/dockerfiles:python

# Install Ansible.
RUN apt-get update && apt-get install -y software-properties-common && apt-add-repository ppa:ansible/ansible && \
	apt-get update && apt-get install -y ansible

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["bash"]

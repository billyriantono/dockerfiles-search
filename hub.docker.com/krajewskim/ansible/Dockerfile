FROM ubuntu:16.04
RUN \
	apt-get update && \
	apt-get install --no-install-recommends -y software-properties-common && \
	apt-add-repository -y ppa:ansible/ansible && \
	apt-get update && \
	apt-get install --no-install-recommends -y ansible python-yaml python-jinja2 python-httplib2 python-keyczar python-paramiko python-setuptools python-pkg-resources git python-pip vim mc man jq && \
	pip install netaddr "pywinrm>=0.1.1" && \
	apt-get clean

#ADD templates/ /

FROM ubuntu:16.04

RUN 	apt-get update && \
	apt-get install -y software-properties-common && \
	apt-add-repository ppa:ansible/ansible && \
	apt-get update && \
	apt-get install -y ansible=2.2.0.0-1ppa~xenial python-pip rsync && \
	rm -rf /var/lib/apt/lists/*

# digitial ocean in newest version is broken
RUN pip install 'dopy==0.3.5'

RUN mkdir /ansible
WORKDIR /ansible

CMD [ "ansible", "--version" ]

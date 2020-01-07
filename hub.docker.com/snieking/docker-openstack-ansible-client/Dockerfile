FROM snieking/docker-openstack-client:latest
LABEL maintainer="viktor@thecuriousdev.org"

USER root
WORKDIR /home/root

RUN apt-get update
RUN apt install -y software-properties-common build-essential libssl-dev libffi-dev
RUN apt-add-repository ppa:ansible/ansible
RUN apt update
RUN apt install -y ansible
RUN pip install shade

USER docker
WORKDIR /home/docker

ENTRYPOINT ["/bin/bash"]
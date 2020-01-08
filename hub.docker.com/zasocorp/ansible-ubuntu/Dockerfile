#Download base image ubuntu 16.04
   FROM ubuntu:16.04
   LABEL maintainer="zauxst" \
    	 maintainer="mstefan"
#Update Ubuntu Software repository
   RUN apt-get update -y && \
       apt-get install -y python-pip && \
       pip install --upgrade pip && \
       python -m pip install ansible
#Show Ansible install location and version
#  RUN ansible --version && \
#      ansible -m ping localhost

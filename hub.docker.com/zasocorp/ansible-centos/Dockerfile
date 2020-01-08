#Download base image centos 7
   FROM centos:7
   LABEL maintainer="zauxst" \
    	 maintainer="mstefan"
#Update Ubuntu Software repository
   RUN yum install -y epel-release && \
       yum install -y python-pip && \
       pip install --upgrade pip && \
       pip install ansible
#Show Ansible install location and version
#  RUN ansible --version && \
#      ansible -m ping localhost

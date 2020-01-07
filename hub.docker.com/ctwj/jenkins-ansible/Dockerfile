FROM jenkins/jenkins

USER root

RUN apt-get update && apt-get install -y python-pip  && apt-get install -y sshpass && rm -rf /var/lib/apt/lists/*
RUN pip install ansible
ADD ./ansible.cfg /etc/ansible/ansible.cfg

USER jenkins

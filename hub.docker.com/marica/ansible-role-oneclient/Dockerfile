FROM indigodatacloud/ubuntu-sshd:16.04

RUN apt-get update -y
RUN apt-get install software-properties-common -y
RUN apt-add-repository ppa:ansible/ansible
RUN apt-get update && \
    apt-get install -y ansible && \
    rm -rf /var/lib/apt/lists/* 
RUN ansible-galaxy install maricaantonacci.oneclient && \
    ansible-playbook /etc/ansible/roles/maricaantonacci.oneclient/tests/test.yml

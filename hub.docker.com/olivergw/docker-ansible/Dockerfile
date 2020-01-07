FROM ubuntu:18.04

RUN apt-get update
RUN apt-get upgrade -y && \
    apt-get install python-pip openssh-client -y

RUN pip install ansible

RUN rm -rf /var/lib/apt/lists/*

CMD [ "ansible-playbook", "--version" ]

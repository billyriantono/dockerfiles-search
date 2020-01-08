FROM python:3

RUN apt-get update\
 && apt-get install -y sshpass\
 && apt-get clean\
 && rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*
RUN pip3 install ansible\
 && pip3 install ansible-lint\
 && pip3 install netaddr\
 && pip3 install boto

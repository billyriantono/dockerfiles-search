FROM python:3.7.4-slim-buster
RUN pip install ansible==2.8.5
RUN apt-get update && apt-get install -y \
  sshpass \
  && rm -rf /var/lib/apt/lists/*
WORKDIR /usr/src/ansible
ENTRYPOINT ["ansible-playbook"]
FROM jenkinsci/ssh-slave

ENV VERSION=2
RUN apt-get update -y
RUN apt-get install -y python
ADD 'https://bootstrap.pypa.io/get-pip.py' get-pip.py
RUN python get-pip.py
RUN pip install ansible
RUN pip install lxml

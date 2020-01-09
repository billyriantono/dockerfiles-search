FROM amazonlinux

RUN yum install traceroute -y
RUN yum install mtr -y
RUN yum install python34 -y

# install pip
RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python3 get-pip.py

RUN pip install --upgrade awscli

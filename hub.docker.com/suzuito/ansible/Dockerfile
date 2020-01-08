FROM centos:7
RUN yum -y update
RUN yum -y install openssh-clients git
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
RUN python get-pip.py
RUN pip install ansible

RUN touch /etc/ssh/ssh_config
RUN echo "Host github.com" >> /etc/ssh/ssh_config
RUN echo "    StrictHostKeyChecking=no" >> /etc/ssh/ssh_config

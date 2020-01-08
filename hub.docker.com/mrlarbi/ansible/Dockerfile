FROM centos:6

# Install dependencies
RUN yum update -y && \
    yum install -y epel-release && \
    yum install -y gcc make libffi-devel openssl-devel python-pip python-devel

#Upgrade pip
RUN pip install --upgrade pip

RUN pip install ansible cryptography && \
    yum install -y iputils iproute
    
CMD [ "ansible-playbook", "--version" ]

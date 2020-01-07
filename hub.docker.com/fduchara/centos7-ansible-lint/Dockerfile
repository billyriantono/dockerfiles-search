FROM centos:7 

RUN yum -y update && yum -y install epel-release \
    && yum -y install ansible python-pip

RUN pip install ansible-lint

# Default command 
CMD ["/bin/bash"]

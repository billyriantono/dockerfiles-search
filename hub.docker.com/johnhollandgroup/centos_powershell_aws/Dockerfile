FROM centos:latest

RUN yum -y update && \
    yum -y install epel-release && \
    yum -y groupinstall "Development Tools" && \
    yum -y install which


# Install Python & pip
RUN yum -y install python3-pip python2-pip
RUN ln -s $(which python3) /usr/local/bin/python3
RUN ln -s $(which python3) /usr/local/bin/python

# Install AWS CLI and boto
RUN pip3 install awscli boto3 && \  
    pip2 install awscli boto3

# Install PowerShell
RUN curl https://packages.microsoft.com/config/rhel/7/prod.repo | tee /etc/yum.repos.d/microsoft.repo
RUN yum install -y powershell

# Install AWS PowerShell
RUN pwsh -command "Install-Module -Name AwsPowerShell.NetCore -Force -Verbose"

# Install Node
RUN curl -sL https://rpm.nodesource.com/setup_10.x | bash -
RUN yum install -y nodejs

# Install Ansible
RUN yum -y install ansible
# RUN pip3.6 install --upgrade pip && pip3.6 install boto3

# Install SAM Local
RUN pip3.6 install aws-sam-cli

# Clean up
RUN yum clean packages && yum clean all

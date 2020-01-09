FROM amazonlinux:latest

# Update 
RUN yum -y update
# Install C and wget
RUN yum install -y gcc-c++ make

# remove chardet 
RUN rm /usr/lib/python2.7/dist-packages/chardet-2.0.1.egg-info
RUN rm -r /usr/lib/python2.7/dist-packages/chardet

# Install pip
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"

RUN python get-pip.py
# Install node
RUN curl --silent --location https://rpm.nodesource.com/setup_8.x | bash -
RUN yum install nodejs -y

CMD ["/bin/bash"]
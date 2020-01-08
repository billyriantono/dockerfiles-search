FROM codered/centos-base:7

MAINTAINER Ronan Gill <ronan.gill@code.red>

# enable proxy
#RUN echo "proxy=http://192.168.1.178:8000" >> /etc/yum.conf

RUN yum install -y epel-release && \
    yum install -y python34 python34-setuptools && \
    curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py" && \
    python3 get-pip.py && \
    rm "get-pip.py" && \
    yum clean all && \
    pip3 install --upgrade mysql-connector-python-rf google-api-python-client gspread

# remove proxy if used above
#RUN  sed -i '/proxy=http/,+1 d' /etc/yum.conf

VOLUME ["/source"]

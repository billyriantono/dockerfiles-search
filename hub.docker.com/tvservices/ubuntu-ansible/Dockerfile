FROM stackbrew/ubuntu:raring
MAINTAINER jamie brim <jamie.brim@samsung.com>

# Start the service
RUN apt-get update
RUN apt-get -y install python-yaml python-jinja2 python-paramiko git build-essential
RUN cd /tmp && git clone https://github.com/ansible/ansible.git && cd ansible && make install

FROM centos:centos7.6.1810
LABEL maintainer "Ivan Goncharov <i.morph@gmail.com>"

RUN yum install sudo -y \
    && sudo yum update -y \
    && sudo yum install epel-release -y \
    && sudo yum install python-pip -y \
    && sudo pip install --upgrade ansible ansible-lint yamllint

CMD [ "bash" ]
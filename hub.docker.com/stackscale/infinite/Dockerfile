FROM centos:7

RUN yum install -y epel-release && yum install -y https://centos7.iuscommunity.org/ius-release.rpm && \
  yum install -y python36u python36u-pip libffi-devel git python36u-devel mysql-devel gcc wget gettext \
  make gcc-c++ mysql tesseract tesseract-langpack-deu

RUN yum localinstall -y https://www.linuxglobal.com/static/blog/pdftk-2.02-1.el7.x86_64.rpm

RUN yum -y install libyaml-devel

RUN pip3.6 --no-cache-dir install --upgrade pip

COPY requirements.txt /tmp
COPY requirements_dev.txt /tmp
RUN pip3.6 --no-cache-dir install -r /tmp/requirements.txt
RUN pip3.6 --no-cache-dir install -r /tmp/requirements_dev.txt

RUN mkdir /var/log/stackscale && chmod 777 /var/log/stackscale

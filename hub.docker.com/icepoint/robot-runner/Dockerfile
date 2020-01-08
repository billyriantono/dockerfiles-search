FROM centos:7

RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && yum clean all
RUN yum install -y python-pip && yum clean all
RUN pip install --upgrade pip
RUN pip install robotframework docutils requests robotframework-requests docker-py

WORKDIR /robot

CMD pybot -o report/output.xml -l report/log.html -r report/index.html -N "Robot tests" suites/*

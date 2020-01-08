FROM maven:3-amazoncorretto-8
LABEL maintainer="Taimos GmbH <info@taimos.de>"

RUN yum -y install python-pip git && pip install awscli cfn-lint awsie

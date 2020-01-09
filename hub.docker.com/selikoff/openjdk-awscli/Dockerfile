FROM openjdk:12
RUN yum update -y
RUN yum install -y python python-pip
RUN pip install --upgrade pip
RUN pip install --no-cache-dir awscli
RUN yum clean packages
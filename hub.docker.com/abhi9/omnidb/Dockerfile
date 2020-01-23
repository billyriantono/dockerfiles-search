FROM centos:7
LABEL maintainer="Abhinav A V<abhai2k@gmail.com>"

RUN yum update -y
RUN yum install wget -y
RUN wget https://omnidb.org/dist/2.14.0/omnidb-server_2.14.0-centos7-amd64.rpm -O /tmp/omnidb-server_2.14.0-centos7-amd64.rpm
RUN rpm -ivh /tmp/omnidb-server_2.14.0-centos7-amd64.rpm
RUN rm -rf /tmp/omnidb-server_2.14.0-centos7-amd64.rpm

EXPOSE 8080
EXPOSE 25482

ENTRYPOINT ["omnidb-server", "-p", "8080", "-w", "25482"]

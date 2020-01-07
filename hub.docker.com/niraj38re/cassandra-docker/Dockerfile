FROM centos:latest



RUN echo -e "[datastax] \nname = DataStax Repo for Apache Cassandra \nbaseurl = http://rpm.datastax.com/community \nenabled = 1 \ngpgcheck = 0" >> "/etc/yum.repos.d/datastax.repo"


COPY ./cassandra-src-pkg /cassandra-src-rpm


RUN yum -y install  deltarpm

#RUN java --version

RUN yum -y install java

RUN rpm -Uvh /cassandra-src-rpm/*.rpm

EXPOSE 9160
EXPOSE 9042

#RUN service cassandra start

CMD service cassandra start

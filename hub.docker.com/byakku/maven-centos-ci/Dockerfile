FROM indigo/centos-jdk8:latest

RUN yum -y install wget

RUN curl --silent --location https://rpm.nodesource.com/setup_10.x | bash 
RUN wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo

RUN yum update -yq
RUN yum install -yq nodejs warn wget apache-maven
RUN npm	install yarn -g


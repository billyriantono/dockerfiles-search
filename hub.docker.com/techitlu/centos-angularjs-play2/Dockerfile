FROM centos:7

RUN yum update -y && yum install -y epel-release nano && yum install -y zip
RUN curl https://setup.ius.io/ | bash
RUN curl -sL https://rpm.nodesource.com/setup_12.x | bash -
RUN yum install -y nodejs
RUN yum install -y java-1.8.0-openjdk-devel
RUN curl https://bintray.com/sbt/rpm/rpm | tee /etc/yum.repos.d/bintray-sbt-rpm.repo
RUN yum install -y sbt
RUN npm install -g @angular/cli
RUN echo "Build OK"
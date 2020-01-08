FROM centos:7.1.1503

RUN yum -y update; yum clean all
RUN curl --silent --location https://rpm.nodesource.com/setup_0.10 | bash -
RUN yum -y install nodejs; yum clean all
RUN yum install gcc-c++ openssl-devel make; yum clean all
RUN npm install -g express-generator

ADD . /src

RUN cd /src; npm install

EXPOSE 8080

CMD ["node", "/src/index.js"]

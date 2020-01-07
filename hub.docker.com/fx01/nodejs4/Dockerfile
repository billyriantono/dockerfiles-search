FROM centos:7
MAINTAINER SugarWu <sugarwu@gmail.com>

RUN yum -y update; yum clean all
RUN yum -y install make gcc gcc-c++; yum clean all
RUN yum -y install epel-release; yum clean all
RUN yum -y install nodejs npm; yum clean all
RUN npm install nodejieba

EXPOSE 3000

CMD ["node", "/usr/share/node/index.js"]
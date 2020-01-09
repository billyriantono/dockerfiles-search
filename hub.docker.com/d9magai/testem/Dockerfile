FROM centos
MAINTAINER d9magai

RUN yum update -y && yum install -y epel-release && yum clean all
RUN yum update -y && yum install -y \
    npm \
    bzip2 \
    freetype \
    fontconfig \
    && yum clean all
RUN npm install -g testem phantomjs
WORKDIR /var/wd

CMD ["testem"]


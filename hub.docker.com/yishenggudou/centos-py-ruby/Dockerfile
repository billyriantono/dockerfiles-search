FROM centos:6
MAINTAINER <timger>
RUN yum -y install screen zlib-dev openssl-devel sqlite-devel bzip2-devel xz-libs mysql libffi-devel graphviz-devel mysql-devel centos-release-SCL epel-release
RUN yum -y install python27 python27-python-devel python27-python-setuptools python27-python-tools npm vim wget nginx apache-maven
RUN scl enable python27 bash
RUN yum --enablerepo=centos-sclo-rh -y install rh-ruby22 rh-ruby22-ruby-devel
RUN scl enable rh-ruby22 bash
RUN npm -g install bower grunt grunt-cli@v1.1.0 i
WORKDIR  /home/admin
RUN npm install -g n
RUN n v8.1.3
RUN wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
RUN yum -y install apache-maven
EXPOSE 80
CMD ["tail", "-F", "-n0", "/etc/hosts"]


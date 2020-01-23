FROM oraclelinux:7

RUN curl https://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/e/epel-release-7-11.noarch.rpm -o epel-release-7-11.noarch.rpm && yum localinstall -y epel-release-7-11.noarch.rpm && rm -f epel-release-7-11.noarch.rpm
RUN curl http://yum.oracle.com/public-yum-ol7.repo -o public-yum-ol7.repo

RUN yum -y update

CMD while true; do sleep 10; done

FROM centos:latest

LABEL maintainer Carl Edquist <edquist@cs.wisc.edu>


RUN mkdir -p /etc/grid-security/certificates /etc/grid-security/vomsdir /etc/grid-security/xrd

RUN yum -y update

# for CA certificates
RUN yum localinstall https://repo.opensciencegrid.org/osg/3.4/osg-3.4-el7-release-latest.rpm -y

RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum install -y fetch-crl osg-ca-scripts


COPY runme.sh /
RUN chmod 755 /runme.sh

CMD [ "/runme.sh" ]


# "ported" from https://registry.hub.docker.com/_/perl/

FROM sherwind/centos-buildpack-deps:centos6 
MAINTAINER Sherwin Daganato <sherwin@daganato.com>

RUN yum -y update && yum clean all
RUN yum -y install perl perl-core && yum clean all
RUN curl -L https://raw.githubusercontent.com/miyagawa/cpanminus/master/cpanm | perl - App::cpanminus \
    && cpanm Carton \
    && rm -rf /root/.cpanm

CMD [ "perl", "-de0" ]

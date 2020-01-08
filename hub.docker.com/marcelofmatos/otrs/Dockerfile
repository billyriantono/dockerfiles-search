FROM juanluisbaptiste/otrs:latest

# postgresql support
RUN yum -y update \
    && yum install -y perl-DBD-Pg \
    && yum clean all
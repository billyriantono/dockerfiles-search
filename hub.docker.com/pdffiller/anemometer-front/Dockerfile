FROM boxinc/anemometer
MAINTAINER Dariya Mykhaylyshyn <mykhaylyshyn.dariya@pdffiller.team>

RUN yum -y install http://www.percona.com/redir/downloads/percona-release/redhat/0.1-6/percona-release-0.1-6.noarch.rpm && \
    yum update percona-release -y && \
    yum -y install percona-toolkit

COPY . /var/www/html


CMD ["/docker-entrypoint.py"]
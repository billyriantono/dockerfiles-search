FROM poklet/cassandra:latest
MAINTAINER Ryan Muller <ryan@kennship.com>
#RUN yum update -y && yum clean all
RUN sed -ri -e 's/^(authenticator:).*/\1 PasswordAuthenticator/' -e 's/^(authorizer:).*/\1 CassandraAuthorizer/' /etc/cassandra/default.conf/cassandra.yaml

ADD entrypoint.sh /entrypoint.sh
CMD sh /entrypoint.sh

VOLUME /var/lib/cassandra

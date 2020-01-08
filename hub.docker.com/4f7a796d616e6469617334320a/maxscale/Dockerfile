FROM ubuntu:latest

ENV VERSION latest

#Trigger to, among others, set Variables and instructions automatically if used to built another image by using the FROM statement.
ONBUILD ENV VERSION $VERSION

RUN apt-get update && apt-get install -y curl bash apt-utils
RUN curl -sS https://downloads.mariadb.com/MariaDB/mariadb_repo_setup | bash -s -- --skip-server --skip-tools  --mariadb-maxscale-version ${VERSION}
RUN apt-get install -y maxscale

RUN mkdir -p /etc/maxscale.d \
    && cp /etc/maxscale.cnf.template /etc/maxscale.d/maxscale.cnf \
    && ln -sf /etc/maxscale.d/maxscale.cnf /etc/maxscale.cnf

# VOLUME for custom configuration
VOLUME ["/etc/maxscale.d"]

ENTRYPOINT ["/usr/bin/maxscale", "-d", "--user=maxscale"]

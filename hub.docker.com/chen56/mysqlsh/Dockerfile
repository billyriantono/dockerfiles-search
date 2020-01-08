#
# mysql-shell
# thanks: https://github.com/elouizbadr/docker-mysql-shell/blob/master/Dockerfile
#

FROM ubuntu:17.04

LABEL maintainer="chen56@msn.com"

ADD files /

RUN set -x \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
       ca-certificates apt-transport-https wget libprotobuf10 libpython2.7 python \
    && rm -rf /var/lib/apt/lists/*

RUN wget https://dev.mysql.com/get/Downloads/MySQL-Shell/mysql-shell_1.0.10-1ubuntu17.04_amd64.deb \
 && DEBIAN_FRONTEND=noninteractive dpkg -i ./mysql-shell_1.0.10-1ubuntu17.04_amd64.deb \
 && rm -f ./mysql-shell_1.0.10-1ubuntu17.04_amd64.deb

ENTRYPOINT ["mysqlsh"]

CMD ["--help"]

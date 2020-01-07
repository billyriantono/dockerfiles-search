FROM fedora:latest

LABEL maintainer.name="Luiz Fernando Pereira"
LABEL maintainer.email="luizfernando@altinfo.com.br"
LABEL maintainer.company="Alternativa Informática"

ARG MYSQL_SERVER_PACKAGE=mysql-community-server-minimal-5.7.24

# Install server
RUN dnf install -y https://repo.mysql.com/mysql-community-minimal-release-el7.rpm \
      dnf-plugins-core \
  && dnf config-manager --enable mysql57-server-minimal \
  && dnf install -y \
      $MYSQL_SERVER_PACKAGE \
      libpwquality \
  && dnf clean all \
  && mkdir /entrypoint-initdb.d

VOLUME /var/lib/mysql

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
COPY healthcheck.sh /healthcheck.sh
RUN chmod +x /healthcheck.sh
COPY my.cnf /etc/my.cnf

ENTRYPOINT ["/entrypoint.sh"]
HEALTHCHECK CMD /healthcheck.sh
EXPOSE 3306 33060
CMD ["mysqld"]
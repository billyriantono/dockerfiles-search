FROM feduxorg/centos:latest
MAINTAINER fedux.org

ENV PG_MAJOR 9.6
ENV PG_MAJOR_PKG 96
ENV PG_RPM_PACKAGE_VERSION 3
ENV PGDATA /var/lib/pgsql/${PG_MAJOR}/data

# Install postgres
RUN groupadd -g 990 -r postgres \
    && useradd -r -g postgres -u 990 postgres \
    && yum install -y http://yum.postgresql.org/${PG_MAJOR}/redhat/rhel-7-x86_64/pgdg-centos${PG_MAJOR_PKG}-${PG_MAJOR}-${PG_RPM_PACKAGE_VERSION}.noarch.rpm \
    && yum install -y postgresql${PG_MAJOR_PKG}-server postgresql${PG_MAJOR_PKG}-contrib \
    && mv /usr/lib/systemd/system/postgresql-${PG_MAJOR}.service /etc/systemd/system/postgresql.service \
    && sed -i -e "s/OOMScoreAdjust/# OOMScoreAdjust/" /etc/systemd/system/postgresql.service \
    && systemctl enable postgresql \
    && mkdir -p ${PGDATA} \
    && mkdir -p /run/postgresql \
    && chown -R postgres ${PGDATA} \
    && chmod g+s /run/postgresql \
    && chown -R postgres:postgres /run/postgresql \
    && yum clean -y all

# Add logrotation
ADD logrotate.conf /etc/logrotate.d/postgresql

# Add init service to setup database on first run
ADD pg-init.sh /usr/local/bin/pg-init.sh
ADD pg-init.service /etc/systemd/system/pg-init.service

RUN chmod +x /usr/local/bin/pg-init.sh \
    && systemctl enable pg-init

# Add backup service
ADD pg-backup.service /etc/systemd/system/pg-backup.service
ADD pg-backup.timer /etc/systemd/system/pg-backup.timer
ADD pg-backup.sh /usr/local/bin/pg-backup.sh

RUN  chmod +x /usr/local/bin/pg-backup.sh \
  && systemctl enable pg-backup.timer

# Add cleanup backup service
ADD pg-backup-cleanup.service /etc/systemd/system/pg-backup-cleanup.service
ADD pg-backup-cleanup.timer /etc/systemd/system/pg-backup-cleanup.timer
ADD pg-backup-cleanup.sh /usr/local/bin/pg-backup-cleanup.sh

RUN  chmod +x /usr/local/bin/pg-backup-cleanup.sh \
  && systemctl enable pg-backup-cleanup.timer

ADD profile.d-environment.sh /etc/profile.d/99-environment.sh
ADD environment.db /etc/pg/environment.db

EXPOSE 5432
VOLUME ["/srv/backup"]

FROM microsoft/mssql-server-linux:latest


#
# Install 'tini', a tiny but valid init for containers
#

RUN       export TINI_VERSION=v0.18.0  \
      &&  wget  https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini  -O /usr/local/sbin/tini  \
      &&  wget  https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini.asc  -O /usr/local/sbin/tini.asc  \
      &&  gpg --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 595E85A6B1B4779EA4DAAEC70B588DFF0527A9B7  \
      &&  gpg --verify /usr/local/sbin/tini.asc  \
      &&  rm /usr/local/sbin/tini.asc  \
      &&  chmod 711 /usr/local/sbin/tini



#
# Setup entrypoint
#

COPY  entrypoint.sh  /usr/local/bin/entrypoint.sh
COPY  entrypoint-initdb.sh  /usr/local/bin/entrypoint-initdb.sh

RUN       chmod 755  /usr/local/bin/entrypoint*.sh  \
      &&  mkdir -p /opt/mssql/share/entrypoint-initdb.d  \
      &&  ln -s /opt/mssql-tools/bin/sqlcmd /usr/local/bin/sqlcmd  \
      &&  ln -s /opt/mssql-tools/bin/bcp /usr/local/bin/bcp

ENTRYPOINT  ["/usr/local/bin/entrypoint.sh"]

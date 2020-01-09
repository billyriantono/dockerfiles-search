# LICENSE UPL 1.0
#
# Copyright (c) 2014-2015 Oracle and/or its affiliates. All rights reserved.
#
FROM oraclelinux:7-slim

ADD https://github.com/bumpx/oracle-instantclient/raw/master/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm /tmp/
ADD https://github.com/bumpx/oracle-instantclient/raw/master/oracle-instantclient12.2-devel-12.2.0.1.0-1.x86_64.rpm /tmp/
ADD https://github.com/bumpx/oracle-instantclient/raw/master/oracle-instantclient12.2-sqlplus-12.2.0.1.0-1.x86_64.rpm /tmp/

RUN  yum -y localinstall /tmp/oracle-instantclient*.rpm && \
     rm -rf /var/cache/yum \
     rm -f /tmp/oracle-instantclient*.rpm && \
     echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient12.2.conf && \
     ldconfig

ENV PATH=$PATH:/usr/lib/oracle/12.2/client64/bin

CMD ["sqlplus", "-v"]
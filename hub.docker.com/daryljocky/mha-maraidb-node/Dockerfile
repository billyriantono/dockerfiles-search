FROM mariadb/server:10.1.36

COPY docker-entrypoint.sh /usr/local/bin/
COPY sshinit.sh /usr/local/bin/
COPY sshauth.sh /usr/local/bin/
COPY ./mha4mysql-node.tar.gz /tmp/

RUN build_deps='ssh sshpass perl libdbi-perl libmodule-install-perl libdbd-mysql-perl make inetutils-ping' \
    && apt-get update \
    && apt-get -y --force-yes install $build_deps \
    && tar -zxf /tmp/mha4mysql-node.tar.gz -C /opt \
    && cd /opt/mha4mysql-node \
    && perl Makefile.PL \
    && make \
    && make install \
    && cd /opt \
    && rm -rf /opt/mha4mysql-* \
    && chmod +x /usr/local/bin/docker-entrypoint.sh \
    && chmod +x /usr/local/bin/sshinit.sh \
    && chmod +x /usr/local/bin/sshauth.sh \
    && apt-get clean 

EXPOSE 22

FROM mysql:5.7

# Modify child mysql to use a different datadir:/var/lib/mysql2 (because /var/lib/mysql wont persist the build)
RUN mkdir -p /var/lib/mysql2 && \
    sed --in-place -e '/^datadir\s*=\s*\/var\/lib\/mysql/cdatadir        = /var/lib/mysql2' /etc/mysql/my.cnf && \
    chown mysql:mysql /var/lib/mysql2

ADD mysql-nzedb.cnf /etc/mysql/conf.d

FROM mysql:5.7.27
FROM th0liveira/base:3.10.2

# MERGE CONTAINER IMAGES -----------------------------------------------------------

COPY --from=mysql:5.7.27 / /
COPY --from=th0liveira/base:3.10.2 /root/.bashrc /root/.bashrc

# PREPARE CONFIGURATIONS -----------------------------------------------------------

# PREPARE DEPENDENCIES -------------------------------------------------------------

# CONFIGURE IMAGE ------------------------------------------------------------------

# -- Modify User / Group
RUN usermod -u 1000 mysql ; groupmod -g 1000 mysql

# -- Config Mysql
ADD config/my.cnf /etc/mysql/my.cnf

# -- Create Paths
RUN \
    mkdir /mnt/run ; chown mysql.mysql -R /mnt/run && \
    mkdir /mnt/data ; chown mysql.mysql -R /mnt/data && \
    mkdir /mnt/log ; chown mysql.mysql -R /mnt/log && \
    mkdir /mnt/dumps ; chown mysql.mysql -R /mnt/dumps

# -- MySQL prepare
COPY mysql-prepare.sh /usr/bin/mysql-prepare
RUN chmod +x /usr/bin/mysql-prepare

# -- MySQL tail
COPY mysql-tail.sh /usr/bin/mysql-tail
RUN chmod +x /usr/bin/mysql-tail

# CLEAR IMAGE ----------------------------------------------------------------------

# DEFAULTS -------------------------------------------------------------------------

# EXPOSE PORT ----------------------------------------------------------------------

EXPOSE 3306

# PREPARE SUPERVISOR FILE ----------------------------------------------------------

RUN echo "[program:mysqld] \n\
command=mysqld --explicit_defaults_for_timestamp \n\
process_name=%(program_name)s_%(process_num)02d \n\
numprocs=1 \n\
autostart=true \n\
autorestart=false \n\
startsecs=0 \n\
redirect_stderr=true \n\
stdout_logfile=/dev/stdout \n\
stdout_logfile_maxbytes=0 " > /etc/supervisord/mysqld.conf

RUN echo "[program:mysqltailf] \n\
command=/usr/bin/mysql-tail \n\
process_name=%(program_name)s_%(process_num)02d \n\
numprocs=1 \n\
autostart=true \n\
autorestart=false \n\
startsecs=0 \n\
redirect_stderr=true \n\
stdout_logfile=/dev/stdout \n\
stdout_logfile_maxbytes=0 " > /etc/supervisord/mysqltailf.conf

# RUN COMMAND ----------------------------------------------------------------------

ENTRYPOINT ["/usr/bin/mysql-prepare"]

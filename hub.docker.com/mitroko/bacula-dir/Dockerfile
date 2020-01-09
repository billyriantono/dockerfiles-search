FROM centos:7
MAINTAINER Dzmitry Stremkouski mitroko@gmail.com

RUN yum -y install epel-release
RUN yum -y install bacula-director supervisor

RUN echo $'[unix_http_server]\n\
file=/var/run/supervisor/supervisor.sock\n\
\n\
[supervisord]\n\
logfile=/var/log/supervisor/supervisord.log\n\
logfile_maxbytes=50MB\n\
logfile_backups=1\n\
loglevel=info\n\
pidfile=/var/run/supervisord.pid\n\
nodaemon=true\n\
minfds=1024\n\
minprocs=200\n\
user=root\n\
\n\
[rpcinterface:supervisor]\n\
supervisor.rpcinterface_factory = supervisor.rpcinterface:make_main_rpcinterface\n\
\n\
[supervisorctl]\n\
serverurl=unix:///var/run/supervisor/supervisor.sock\n\
\n\
[program:bacula-dir]\n\
command=/usr/sbin/bacula-dir -c /etc/bacula/bacula-dir.conf -f\n\
numprocs=1\n\
autostart=true\n\
autorestart=true\n\
startsecs=10\n\
startretries=1\n\
user=bacula\n\
stdout_logfile=/var/log/supervisor/bacula-dir.stdout.log\n\
stdout_logfile_maxbytes=1MB\n\
stdout_logfile_backups=10\n\
stderr_logfile=/var/log/supervisor/bacula-dir.stderr.log\n\
stderr_logfile_maxbytes=1MB\n\
stderr_logfile_backups=10\n\
' > /usr/local/etc/supervisord.conf

RUN sed -i 's/PidDirectory.*/PidDirectory = \/var\/run\/bacula/' /etc/bacula/bacula-dir.conf
RUN mkdir -p /var/run/bacula && chown bacula: /var/run/bacula -R
RUN cp /etc/bacula/bacula-dir.conf /usr/local/share/bacula-dir.conf && cp /etc/bacula/query.sql /usr/local/share/bacula-dir.query.sql
RUN echo $'#!/bin/bash\n\
[ -f /etc/bacula/bin/dir_pre_start.sh ] && /etc/bacula/bin/dir_pre_start.sh\n\
[ ! -f /etc/bacula/bacula-dir.conf ] && cp /usr/local/share/bacula-dir.query.sql /etc/bacula/query.sql && chown bacula: /etc/bacula/query.sql \n\
[ ! -f /etc/bacula/bacula-dir.conf ] && cp /usr/local/share/bacula-dir.conf /etc/bacula/bacula-dir.conf && chown bacula: /etc/bacula/bacula-dir.conf \n\
find /var/run/ -iname *.pid -delete\n\
/usr/bin/supervisord -n -c /usr/local/etc/supervisord.conf\n\
' > /usr/local/bin/entrypoint.sh && chmod 0755 /usr/local/bin/entrypoint.sh

EXPOSE 9101/tcp
VOLUME ["/etc/bacula"]
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

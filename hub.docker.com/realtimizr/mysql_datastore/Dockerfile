FROM busybox

ADD https://dl.dropboxusercontent.com/u/15675714/phpbb.sql /tmp/phpbb.sql
ADD undump.sh /tmp/undump_phpbb.sh
RUN \
  adduser -H -D mysql mysql && \
  mkdir /var/lib && \
  mkdir /var/lib/mysql && \
  chown -R mysql:mysql /var/lib/mysql && \
  mkdir /var/backup && \
  cp /tmp/phpbb.sql /var/backup && \
  cp /tmp/undump_phpbb.sh /var/backup && \
  rm /tmp/phpbb.sql && \
  rm /tmp/undump_phpbb.sh
VOLUME /var/lib/mysql
VOLUME /var/backup
CMD /bin/sh

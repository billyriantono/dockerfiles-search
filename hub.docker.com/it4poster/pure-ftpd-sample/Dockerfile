FROM stilliard/pure-ftpd

ENV USER ftpuser
ENV PASSWORD qwerty
ENV FTP_PATH /srv/ftp/
ENV PUBLICHOST localhost

CMD echo "$PASSWORD\n$PASSWORD" | pure-pw useradd $USER -u ftpuser -d $FTP_PATH && pure-pw mkdb && /usr/sbin/pure-ftpd -c 50 -C 10 -l puredb:/etc/pure-ftpd/pureftpd.pdb -E -j -R -P $PUBLICHOST -p 30000:30009

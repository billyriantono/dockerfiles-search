FROM stilliard/pure-ftpd

VOLUME /home/ftpusers /etc/pure-ftpd

CMD /usr/sbin/pure-ftpd -c 50 -C 10 -l puredb:/etc/pure-ftpd/pureftpd.pdb -E -j -R -P $PUBLICHOST -p 30000:30009

FROM mauromussin/myscriptr:recupero_RT-pgsql
COPY . /usr/local/src/myscripts
WORKDIR /usr/local/src/myscripts
RUN /usr/sbin/service rsyslog start
CMD ["./launch_recuperoRT-new.sh"]

FROM codejuggle/base:latest

# Add repository to allow installing of latest version
RUN echo "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main" >> /etc/apt/sources.list
RUN wget -q -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add -

# Update system
RUN apt-get update; apt-get -y upgrade

# Install postgresql
ENV PGVERSION 9.6
ENV PGVERSIONFULL 9.6.1
RUN apt-get -y install --no-install-recommends postgresql-$PGVERSION postgresql-server-dev-$PGVERSION postgresql-contrib-$PGVERSION postgresql-plperl-$PGVERSION

# Install the postgresql debugger
RUN apt-get -y install --no-install-recommends gcc git make libkrb5-dev libreadline-dev libssl-dev zlib1g-dev
RUN wget -q ftp://ftp.postgresql.org/pub/source/v$PGVERSIONFULL/postgresql-$PGVERSIONFULL.tar.gz
RUN tar xzf postgresql-$PGVERSIONFULL.tar.gz
RUN cd postgresql-$PGVERSIONFULL && USE_PGXS=1 ./configure && USE_PGXS=1 make && cd contrib && make
RUN cd postgresql-$PGVERSIONFULL/contrib && git clone git://git.postgresql.org/git/pldebugger.git
RUN cd postgresql-$PGVERSIONFULL/contrib/pldebugger && USE_PGXS=1 make && USE_PGXS=1 make install
RUN rm -f postgresql-$PGVERSIONFULL.tar.gz && rm -rf postgresql-$PGVERSIONFULL

# Install bucardo for postgresql replication
RUN apt-get -y install --no-install-recommends libboolean-perl libdbd-pg-perl libdbi-perl libdbix-safe-perl
ENV BUCARDOVERSION 5.4.1
RUN wget -q http://bucardo.org/downloads/Bucardo-$BUCARDOVERSION.tar.gz
RUN tar xzf Bucardo-$BUCARDOVERSION.tar.gz
RUN cd Bucardo-$BUCARDOVERSION && perl Makefile.PL
RUN cd Bucardo-$BUCARDOVERSION && make && make install
RUN mkdir /var/run/bucardo /var/log/bucardo
RUN rm -f Bucardo-$BUCARDOVERSION.tar.gz && rm -rf Bucardo-$BUCARDOVERSION

# Update configuration
ADD pg_hba.conf /etc/postgresql/$PGVERSION/main/pg_hba.conf

# Add service script
ADD run.sh /etc/service/postgresql/run
RUN chmod 777 /etc/service/postgresql/run
ADD run_pwsetter.sh /etc/service/postgresql_pwsetter/run
RUN chmod 777 /etc/service/postgresql_pwsetter/run

WORKDIR /var/lib/postgresql/

EXPOSE 5432

# clean up not needed services and temp files
RUN rm -rf /etc/service/cron /etc/service/sshd /etc/my_init.d/00_regen_ssh_host_keys.sh /etc/service/syslog-ng /etc/service/syslog-forwarder
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD ["/sbin/my_init"]

FROM debian:stretch

ADD http://www.quicklz.com/qpress-11-linux-x64.tar /tmp

RUN apt-get update \
	&& apt-get install -y wget lsb-release rsync perl libcurl4-openssl-dev libaio1  libatomic1 libev4 libdbd-mysql-perl \
	&& wget https://www.percona.com/downloads/Percona-XtraBackup-2.4/Percona-XtraBackup-2.4.15/binary/debian/stretch/x86_64/percona-xtrabackup-24_2.4.15-1.stretch_amd64.deb \
	&& dpkg -i percona-xtrabackup-24_2.4.15-1.stretch_amd64.deb \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm percona-xtrabackup-24_2.4.15-1.stretch_amd64.deb \
	&& tar -C /usr/local/bin -xf /tmp/qpress-11-linux-x64.tar qpress
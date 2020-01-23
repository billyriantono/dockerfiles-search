FROM	dnraikes/kali-msf
MAINTAINER	Donald Raikes <don.raikes@oracle.com>
RUN	apt-get -yq update 
RUN	apt-get install -y rsync libhiredis-dev build-essential devscripts dpatch libassuan-dev \
	libglib2.0-dev libgpgme11-dev libpcre3-dev libpth-dev libwrap0-dev libgmp-dev libgmp3-dev \
	quilt cmake pkg-config \
	libssh-dev libglib2.0-dev libpcap-dev libgpgme11-dev uuid-dev bison libksba-dev \
	doxygen sqlfairy xmltoman sqlite3 libsqlite3-dev wamerican rsyslog redis-server \
 	libmicrohttpd-dev libxml2-dev libxslt1-dev xsltproc libssh2-1-dev libldap2-dev autoconf nmap libgnutls28-dev supervisor \
	subversion nano vim mlocate \
	g++ gcc-mingw-w64  \
  	perl-base heimdal-dev libpopt-dev 
RUN	apt-get clean 
RUN	mkdir /root/bin
COPY	bin/*.sh	/root/bin/
RUN	echo "export PATH=.:$HOME:$HOME/bin:$PATH" >> /root/.bashrc
RUN	chmod +x /root/bin/*.sh
RUN	/root/bin/build_all.sh

FROM		debian:jessie
MAINTAINER	Victor M. Varela <v.varela@neartechnologies.com>

RUN		apt-get update \
	&&	apt-get install -y --no-install-recommends python-pyftpdlib \
	&&	apt-get clean \
	&&	rm -rf /var/lib/apt/lists/*

COPY		server.py /server.py
RUN		mkdir /ftp

ENV		FTP_IPADDRESS		0.0.0.0
ENV		FTP_USERS		BOB,JANE
ENV		FTP_BOB_USERNAME	bob
ENV		FTP_BOB_PASSWORD	mynameisbob
ENV		FTP_BOB_HOME		/ftp/bob
ENV		FTP_JANE_USERNAME	jane
ENV		FTP_JANE_PASSWORD	hellobob
ENV		FTP_JANE_HOME		/ftp/jane

CMD		["python", "server.py"]


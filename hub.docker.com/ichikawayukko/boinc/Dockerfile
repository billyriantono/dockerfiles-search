FROM	centos:7.6.1810
RUN	yum install -y epel-release && \
	yum install -y boinc-client && \
	echo '#!/bin/sh' > /usr/local/bin/entrypoint.sh && \
	echo 'chown boinc:boinc /var/lib/boinc' >> /usr/local/bin/entrypoint.sh && \
	echo 'exec "$@"' >> /usr/local/bin/entrypoint.sh && \
	chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT ["entrypoint.sh"]
WORKDIR	/var/lib/boinc
CMD	["su", "-s", "/bin/sh", "-", "boinc", "-c", "boinc"]


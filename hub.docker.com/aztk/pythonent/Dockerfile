FROM		autoglass/base
ENV			DEBIAN_FRONTEND=noninteractive
ENV			TERM=xterm
RUN			apt-get update && \
			apt-get -y install slapd ldap-utils ldapscripts
HEALTHCHECK	--interval=1m --timeout=3s CMD nc -zv 127.0.0.1 389 || exit 1

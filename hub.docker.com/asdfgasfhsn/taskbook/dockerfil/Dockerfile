FROM ubuntu:trusty
MAINTAINER ASCDC <asdc.sinica@gmail.com>

ADD run.sh /run.sh

RUN DEBIAN_FRONTEND=noninteractive && \
	chmod +x /*.sh && \
	apt-get update && \
	apt-get -y upgrade && \
	locale-gen en_US.UTF-8 && \
	export LANG=en_US.UTF-8 && \
	apt-get install -y snmpd && \
	sed -i "s/agentAddress.*/agentAddress\tudp:0.0.0.0:161/g" /etc/snmp/snmpd.conf && \
	sed -i "s/sysLocation.*/sysLocation\tundefined/g" /etc/snmp/snmpd.conf && \
	sed -i "s/sysContact.*/sysContact\tasdc.sinica@gmail.com/g" /etc/snmp/snmpd.conf && \
	sed -i -E "s/view(.*)/#view\1/g" /etc/snmp/snmpd.conf && \
	echo "view	systemonly	included	.1 ">>/etc/snmp/snmpd.conf

EXPOSE 161
WORKDIR /etc/snmp/
ENTRYPOINT ["/run.sh"]
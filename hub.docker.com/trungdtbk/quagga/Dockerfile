FROM osrg/quagga

RUN apt update && apt install --upgrade -q iperf3 iptables fping
RUN mv /usr/sbin/tcpdump /usr/bin/tcpdump
ADD 10-network-security.conf /etc/sysctl.d/

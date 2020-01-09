from webwurst/ubuntu
run apt-get update

# haproxy
run apt-get -y install haproxy
run cd /tmp && curl -O http://mirrors.kernel.org/ubuntu/pool/main/h/haproxy/haproxy_1.5.1-1_amd64.deb
run cd /tmp && curl -O http://mirrors.kernel.org/ubuntu/pool/main/i/init-system-helpers/init-system-helpers_1.19_all.deb
run dpkg -i /tmp/*.deb

# config
run echo "ENABLED=1" > /etc/default/haproxy
add haproxy.cfg /etc/haproxy/

# clean up
run rm -fR /tmp/*

expose 80 443
cmd ["/usr/sbin/haproxy", "-f", "/etc/haproxy/haproxy.cfg", "-db"]

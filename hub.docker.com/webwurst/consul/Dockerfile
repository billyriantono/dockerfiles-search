from webwurst/ubuntu
run apt-get update

# consul
run curl -L https://dl.bintray.com/mitchellh/consul/0.3.0_linux_amd64.zip > /tmp/consul.zip && \
  cd /usr/local/bin && unzip /tmp/consul.zip && chmod u+x /usr/local/bin/consul

# consul-ui
run curl -L https://dl.bintray.com/mitchellh/consul/0.3.0_web_ui.zip > /tmp/consul-ui.zip && \
  cd /opt && unzip /tmp/consul-ui.zip

# config
add consul.json /etc/consul/

# clean up
run rm -fR /tmp/*

volume ["/var/consul"]
cmd ["/usr/local/bin/consul", "agent", "-config-dir=/etc/consul"]
expose 8300 8301 8302 8400 8500 53/udp

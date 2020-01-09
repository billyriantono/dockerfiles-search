FROM busybox:ubuntu-14.04
MAINTAINER william0wang

# Install ngrok
COPY client_linux_amd64 /bin/kcptun
RUN chmod 755 /bin/kcptun

CMD kcptun -l :${kcp_out_port} -r ${kcp_in_addr} --crypt ${kcp_crypt} --key ${kcp_key} ${kcp_options} --mode ${kcp_mode}

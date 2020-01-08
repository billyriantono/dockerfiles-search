FROM kylemanna/openvpn

RUN apk add --update --no-cache openssh openrc && \
    ssh-keygen -f /etc/ssh/ssh_host_rsa_key -N '' -t rsa && \
    ssh-keygen -f /etc/ssh/ssh_host_dsa_key -N '' -t dsa && \
    mkdir -p /var/run/sshd && \
    mkdir -p /run/openrc && \
    touch /run/openrc/softlevel

RUN rc-update add sshd

# ADD https://github.com/ailinykh.keys /root/.ssh/authorized_keys

ADD entrypoint.sh /root/entrypoint.sh
RUN chmod a+x /root/entrypoint.sh

CMD ["/root/entrypoint.sh"]
FROM ilemonrain/centos-sshd
COPY shadowsocks.sh /usr/sbin/
RUN chmod +x /usr/sbin/shadowsocks.sh
COPY init-docker /usr/sbin/init-docker
RUN chmod +x /usr/sbin/init-docker

ENTRYPOINT [ "/usr/sbin/init-docker" ]
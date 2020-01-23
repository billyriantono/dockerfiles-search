FROM ubuntu:18.10
RUN cd ~;\
    apt-get update ;\
    apt-get upgrade -y;\
    apt-get install  shadowsocks-libev simple-obfs supervisor openssh-server  -y;\
    mkdir /var/run/sshd;\
    echo 'root:root' |chpasswd;\
#    ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key;\
#    ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key;\
    sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config;\
    sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config;\
    mkdir /root/.ssh;\
    apt-get clean;\
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*;\
    mkdir -p /var/log/supervisor ;\
    echo "[supervisord]">  /etc/supervisord.conf ;\
    echo "nodaemon=true">>  /etc/supervisord.conf ;\
    echo "[program:sshd]">>  /etc/supervisord.conf ;\
    echo "command=/usr/sbin/sshd -D">>  /etc/supervisord.conf ;\
    echo "[program:ss]">>  /etc/supervisord.conf ;\
    echo "command=/usr/bin/ss-server -s 0.0.0.0 -p 51200 -k 0ooOOO@ -m aes-256-gcm -t 300 -d 8.8.8.8 --fast-open -u --plugin obfs-server --plugin-opts obfs=http;fast-open;failover=bing.com">>  /etc/supervisord.conf
# COPY supervisord.conf  
EXPOSE 22/tcp
EXPOSE 51200/tcp
EXPOSE 51200/udp
# CMD ["/bin/sh","-c","/usr/bin/ss-server -s $SERVER_ADDR -p $SERVER_PORT -k $PASSWORD -m $METHOD -t $TIMEOUT -d $DNS_ADDR --fast-open -u $OPTIONS"]
CMD ["/usr/bin/supervisord"]  

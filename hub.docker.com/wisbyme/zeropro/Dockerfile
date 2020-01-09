FROM wisbyme/python2

LABEL maintainer="letssudormrf"

ENV PATH /home/html:$PATH
COPY 01_start_zeropro.sh /tmp/01_start_zeropro.sh
COPY shadowsocks-all.sh  /bin/shadowsocksr

#ENV HTML_PORT
#ENV SSH_AUTHORIZED_KEYS    & SSH_PORT
#ENV NQNEW_TOKEN_KEYS 

#ENV SSRCFG_PORT            & SSRCFG_PASSWD        &
#    SSRCFG_CIPHER          & SSRCFG_PROTOCOL      &
#    SSRCFG_OBFS
#ENV SS_CFGS_ENABLE         & SHADOWSOCKS_CFGS_{port}

#ENV FRP_TOKEN_KEYS         & FRP_BIND_PORT        &
#    FRP_BIND_UDP_PORT      & FRP_RPIALLOW_PORTS   &
#    FRP_VHOST_HTTP_PORT    & FRP_VHOST_HTTPS_PORT & 
#    FRP_DASHBOARD_PORT     & FRP_DASHBOARD_USER   &
#    FRP_DASHBOARD_PASSWD 

RUN apt-get update -y \
 && apt-get install -y --no-install-recommends \
    net-tools wget virt-what kmod iputils-ping iproute2 arp-scan nmap  \
#   gettext unzip gzip curl git qrencode \
#   build-essential python python-dev python-setuptools \
#   openssl libssl-dev autoconf automake libtool gcc make perl cpio \
#   libpcre3 libpcre3-dev zlib1g-dev libev-dev libc-ares-dev \
 && mkdir -p /home/html /home/bin \
 && chmod +x /bin/shadowsocksr \
 && ln -s /bin/shadowsocksr /home/bin/shadowsocksr \
 && wget --tries=0 --quiet https://raw.githubusercontent.com/programs/superssr/master/baseimage-xenialmu.tar.gz -O /tmp/zeropro.tar.gz \
 && tar -C / -xzf /tmp/zeropro.tar.gz \
 && rm -rf /usr/local/shadowsocksr/ /usr/local/shadowsocks /tmp/zeropro.tar.gz /etc/my_init.d/._01_start_zeropro.sh \
 && wget --no-check-certificate -c -t3 -T60 -O /home/bin/shadowsocksr-3.2.2.tar.gz https://github.com/shadowsocksrr/shadowsocksr/archive/3.2.2.tar.gz \
 && wget --no-check-certificate -c -t3 -T60 -O /etc/init.d/shadowsocks-r https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocksR-debian \
 && tar -C /home/bin/ -xzf /home/bin/shadowsocksr-3.2.2.tar.gz \
 && mv /home/bin/shadowsocksr-3.2.2/shadowsocks /usr/local/ \
 && chmod +x /etc/init.d/shadowsocks-r \
 && update-rc.d -f shadowsocks-r defaults \
 && rm -rf /home/bin/shadowsocksr-3.2.2.tar.gz /home/bin/shadowsocksr-3.2.2/ \
 && touch /etc/ld.so.conf.d/html.conf \
 && echo "/home/html" >> /etc/ld.so.conf.d/html.conf \
 && /sbin/ldconfig \
 && echo "export PATH=$PATH:/home/html" >> ~/.bashrc \
 && mv /tmp/01_start_zeropro.sh /etc/my_init.d/01_start_zeropro.sh \
 && chmod +x /etc/my_init.d/01_start_zeropro.sh \
 && apt-get autoremove -y \
 && apt-get autoclean -y \
 && rm -rf /var/cache/apt/* /var/lib/apt/lists/* /tmp/* /var/tmp/* \
 && /sbin/install_clean

WORKDIR /home

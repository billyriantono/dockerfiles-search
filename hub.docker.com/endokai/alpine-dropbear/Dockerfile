FROM alpine as builder
MAINTAINER endokai
RUN set -ex && echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories &&  apk update
RUN set -ex && apk add libsodium libsodium-dev mbedtls mbedtls-dev pcre  linux-headers  libev libev-dev libcork@testing libcorkipset@testing c-ares libbloom@testing autoconf automake libtool gettext c-ares-dev pkgconfig gcc g++ pcre-dev make wget curl git bash rng-tools libuv libuv-dev cmake gtest gtest-dev curl-dev libevent-dev
RUN  cd /root && /usr/bin/curl --silent "https://api.github.com/repos/Yelp/dumb-init/releases/latest"|grep browser_download_url|grep -Eo "https.*amd64"|head -1|wget --no-check-certificate -O /bin/dumb-init -i - && \
   cd /root && /usr/bin/curl --silent "https://api.github.com/repos/shadowsocks/shadowsocks-libev/releases/latest"|grep -Eo "https://github.com/shadowsocks.*\.tar\.gz"|wget --no-check-certificate -i - && \
   cd /root && /usr/bin/curl --silent "https://api.github.com/repos/wangyu-/udp2raw-tunnel/releases/latest" | grep -Eo "https.*\.tar\.gz" | wget --no-check-certificate -O udp2raw.tar.gz -i - && \
   cd /root && /usr/bin/curl --silent "https://api.github.com/repos/wangyu-/UDPspeeder/releases/latest" | grep -Eo "https.*\.tar\.gz" | wget --no-check-certificate -O udpspeeder.tar.gz -i -
RUN set -ex && cd /root && tar -zxvf shadowsocks-libev*.tar.gz && cd /root/shadowsocks-libev* && \
   ./configure --disable-documentation --disable-dependency-tracking &&  make 
RUN set -ex && cd /root && git clone https://github.com/shadowsocks/simple-obfs && \
   cd /root/simple-obfs/ && git submodule update --init --recursive && ./autogen.sh && \
   ./configure --disable-documentation && make
RUN set -ex && cd /root && wget -O /root/doh.zip https://github.com/aarond10/https_dns_proxy/archive/master.zip && \
   cd /root && unzip /root/doh.zip && cd /root/https_dns_proxy-master && cmake . && make
RUN set -ex && cd /root &&  git clone https://github.com/liudf0716/xkcptun.git && mkdir xkcptun/build && cd xkcptun/build &&  cmake .. && make
RUN set -ex && cd /root && tar -zxvf udpspeeder.tar.gz &&  tar -zxvf udp2raw.tar.gz

RUN mkdir /usr/local/src && apk update && apk add binutils build-base readline-dev openssl-dev ncurses-dev git cmake
RUN apk add gnu-libiconv --update-cache --repository http://dl-cdn.alpinelinux.org/alpine/edge/testing/ --allow-untrusted
ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so
WORKDIR /usr/local/src
RUN git clone https://github.com/SoftEtherVPN/SoftEtherVPN.git
WORKDIR /usr/local/src/SoftEtherVPN
RUN git submodule update  --init --recursive && ./configure && make -C tmp


FROM alpine
MAINTAINER endokai
ENV KEY="ssh-rsa-YourSSHPublicKey"
ENV EXEC="ZHJvcGJlYXIgLVIgLUYgLUUgLXMK"
EXPOSE 22
COPY --from=builder /root/https_dns_proxy-master/https_dns_proxy /sbin/https_dns_proxy
COPY --from=builder /root/speederv2_amd64 /sbin/udpspeeder
COPY --from=builder /root/udp2raw_amd64_hw_aes /sbin/udp2raw
COPY --from=builder /root/simple-obfs/src/obfs-local /sbin/obfs-local
COPY --from=builder /root/simple-obfs/src/obfs-server /sbin/obfs-server
COPY --from=builder /root/shadowsocks-libev-*/src/ss-local  /sbin/ss-local
COPY --from=builder /root/shadowsocks-libev-*/src/ss-manager /sbin/ss-manager
COPY --from=builder /root/shadowsocks-libev-*/src/ss-nat /sbin/ss-nat
COPY --from=builder /root/shadowsocks-libev-*/src/ss-redir /sbin/ss-redir
COPY --from=builder /root/shadowsocks-libev-*/src/ss-server /sbin/ss-server
COPY --from=builder /root/shadowsocks-libev-*/src/ss-tunnel /sbin/ss-tunnel
COPY --from=builder /root/xkcptun/build/xkcp_client /sbin/xkcp_client
COPY --from=builder /root/xkcptun/build/xkcp_spy /sbin/xkcp_spy
COPY --from=builder /root/xkcptun/build/xkcp_server /sbin/xkcp_server
COPY --from=builder /bin/dumb-init /bin/dumb-init
RUN set -ex &&  echo "@testing http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && apk update
RUN set -ex && apk add libsodium mbedtls pcre libev libcork@testing libcorkipset@testing c-ares libbloom@testing gettext  wget curl libevent bash rng-tools dropbear rsync libuv gtest
RUN set -ex && echo -n IyEvYmluL2Jhc2gKd2hpbGUgOgpkbwplY2hvICIke0tFWX0iID4+IC9yb290Ly5zc2gvYXV0aG9yaXplZF9rZXlzCmVjaG8gLW4gIiR7RVhFQ30ifGJhc2U2NCAtZHxiYXNoCnNsZWVwIDEwCmRvbmUK | base64 -d > /bin/run.sh
RUN chmod a+x /bin/run.sh /sbin/xkcp_server /sbin/xkcp_spy /sbin/xkcp_client /sbin/ss-tunnel /sbin/ss-server /sbin/ss-redir /sbin/ss-nat /sbin/ss-manager /sbin/ss-local  /sbin/obfs-server /sbin/obfs-local /sbin/udp2raw /sbin/udpspeeder /sbin/https_dns_proxy /bin/dumb-init && \
   mkdir /etc/dropbear && mkdir /root/.ssh

ENV LD_PRELOAD /usr/lib/preloadable_libiconv.so
ENV LD_LIBRARY_PATH /root
WORKDIR /root/
RUN ln -s /mnt/vpn_server.config vpn_server.config && mkdir /mnt/backup.vpn_server.config && \
        ln -s /mnt/backup.vpn_server.config backup.vpn_server.config &&\
        ln -s /mnt/lang.config lang.config
COPY --from=builder /usr/local/src/SoftEtherVPN/build /root/

CMD ["/bin/run.sh"]
ENTRYPOINT ["/bin/dumb-init"]

FROM ubuntu

RUN apt-get update && apt-get install -y wget gcc g++ libssl-dev make

WORKDIR /root/nmap-build
WORKDIR /root

RUN wget https://nmap.org/dist/nmap-7.70.tar.bz2 && tar jxf nmap-7.70.tar.bz2

WORKDIR /root/nmap-7.70

RUN ./configure --prefix=/ --with-liblua=included && make && make DESTDIR=/root/nmap-build install

WORKDIR /root/nmap-build/bin

RUN strip nmap
RUN strip ncat
RUN strip nping

FROM scratch

WORKDIR /bin
WORKDIR /lib
WORKDIR /lib64
WORKDIR /share

WORKDIR /

COPY --from=0 /root/nmap-build/bin/nmap /bin/
COPY --from=0 /root/nmap-build/share/nmap /share/
COPY --from=0 /usr/lib/x86_64-linux-gnu/libcrypto.so* /lib/
COPY --from=0 /usr/lib/x86_64-linux-gnu/libssl.so* /lib/
COPY --from=0 /usr/lib/x86_64-linux-gnu/libstdc++.so.6 /lib/
COPY --from=0 /lib/x86_64-linux-gnu/libc.so.6 /lib/
COPY --from=0 /lib/x86_64-linux-gnu/libdl.so.2 /lib/
COPY --from=0 /lib/x86_64-linux-gnu/libm.so.6 /lib/
COPY --from=0 /lib/x86_64-linux-gnu/libgcc_s.so.1 /lib/
COPY --from=0 /lib/x86_64-linux-gnu/libpthread.so.0 /lib/
COPY --from=0 /lib64/ld-linux-x86-64.so.2 /lib64/

ENTRYPOINT ["/bin/nmap"]

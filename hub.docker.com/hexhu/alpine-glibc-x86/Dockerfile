FROM alpine:latest

RUN apk add --update --no-cache wget tar xz
RUN wget http://mirrors.edge.kernel.org/archlinux/core/os/x86_64/lib32-glibc-2.29-4-x86_64.pkg.tar.xz
RUN mkdir -p lib32-glibc /etc/ld.so.conf.d /usr/include/ /usr/lib32/
RUN tar xf lib32-glibc-2.29-4-x86_64.pkg.tar.xz -C lib32-glibc
RUN cp -i lib32-glibc/etc/ld.so.conf.d/lib32-glibc.conf /etc/ld.so.conf.d/
RUN cp -i lib32-glibc/usr/lib/ld-linux.so.2 /lib/ld-linux.so.2
RUN cp -ai lib32-glibc/usr/include/ /usr/
RUN cp -ai lib32-glibc/usr/lib32 /usr/
RUN ldconfig /usr /usr/lib
RUN rm -rf lib32-glibc/ lib32-glibc-2.29-4-x86_64.pkg.tar.xz
RUN apk del wget tar xz

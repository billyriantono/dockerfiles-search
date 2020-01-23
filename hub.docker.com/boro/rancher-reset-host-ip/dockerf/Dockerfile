FROM alpine:latest
LABEL MAINTAINER="Volker Faas <bluezdrive@volkerfaas.de>"
RUN wget -q --no-check-certificate https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.27-r0/glibc-2.27-r0.apk -O /tmp/glibc-2.27-r0.apk && \
    wget -q --no-check-certificate https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.27-r0/glibc-bin-2.27-r0.apk -O /tmp/glibc-bin-2.27-r0.apk && \
    mkdir -p /tmp/zlib && \
    wget -qO- http://ftp5.gwdg.de/pub/linux/archlinux/core/os/x86_64//zlib-1:1.2.11-3-x86_64.pkg.tar.xz -O /tmp/zlib-1-1.2.11-3-x86_64.pkg.tar.xz && \
    tar -xf /tmp/zlib-1-1.2.11-3-x86_64.pkg.tar.xz -C /tmp/zlib/ && \
    apk add --allow-untrusted --no-cache /tmp/glibc-2.27-r0.apk /tmp/glibc-bin-2.27-r0.apk && \
    rm /tmp/glibc-2.27-r0.apk /tmp/glibc-bin-2.27-r0.apk /tmp/zlib-1-1.2.11-3-x86_64.pkg.tar.xz && \
    /sbin/ldconfig /lib /usr/glibc/usr/lib && \
    cp /tmp/zlib/usr/lib/libz.so.1.2.11 /usr/glibc-compat/lib && \
    /usr/glibc-compat/sbin/ldconfig && \
    rm -rf /tmp/zlib && \
    mkdir -p /opt/java && \
    wget -q --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/10.0.2+13/19aef61b38124481863b1413dce1855f/serverjre-10.0.2_linux-x64_bin.tar.gz -O /opt/java/serverjre-10.0.2_linux-x64_bin.tar.gz && \
    tar -xzf /opt/java/serverjre-10.0.2_linux-x64_bin.tar.gz -C /opt/java/ && \
    rm /opt/java/serverjre-10.0.2_linux-x64_bin.tar.gz
ENV JAVA_HOME /opt/java/jdk-10.0.2
ENV PATH $PATH:$JAVA_HOME/bin
CMD []
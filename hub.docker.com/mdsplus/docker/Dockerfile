from multiarch/alpine:x86_64-v3.9
RUN echo "http://dl-3.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories; \
    echo "http://dl-3.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories; \
    apk add --update alpine-keys; \
    apk add bash automake make git rsync tar wget python py-setuptools \
       gcc g++ gfortran binutils libgcc libstdc++ libquadmath libgfortran \
       libdc1394 libdc1394-dev libraw1394 libraw1394-dev  \
       readline readline-dev python-dev \
       motif-dev libxml2-dev libxml2 curl-dev curl freetds-dev dev86 \
       py2-numpy openjdk8 openjdk8-jre-lib hdf5 hdf5-dev alpine-sdk \
       perl-test-harness valgrind py-pip ; \
    ln -sf /usr/lib/bcc/include/sys/cdefs.h /usr/include/sys/; \
    pip2 install nose tap tap.py; \
    wget -P /etc/apk/keys/ http://www.mdsplus.org/dist/mdsplus@mdsplus.org-589e05b6.rsa.pub; \
    echo "PACKAGER_PRIVKEY=\"/sign_keys/mdsplus@mdsplus.org-589e05b6.rsa\"\n" > abuild.conf

ENV JDK_DIR=/usr/lib/jvm/java-1.8-openjdk


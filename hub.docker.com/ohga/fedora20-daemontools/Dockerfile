FROM fedora:20
MAINTAINER k_ohga

RUN yum install -y gcc make binutils cpp glibc-devel glibc-headers kernel-headers libgomp libmpc mpfr && \
  cd /usr/local/src && \
  curl http://cr.yp.to/ucspi-tcp/ucspi-tcp-0.88.tar.gz | tar zxv && \
  curl http://cr.yp.to/cdb/cdb-0.75.tar.gz | tar zxv && \
  cd ucspi-tcp-0.88 && \
    echo 'gcc -O2 --include /usr/include/errno.h' > conf-cc && \
    make && make setup && make check && \
  cd ../cdb-0.75 && \
    echo 'gcc -O2 --include /usr/include/errno.h' > conf-cc && \
    make && make setup && make check && \
  mkdir -p /package && chmod 1755 /package && cd /package && \
  curl http://cr.yp.to/daemontools/daemontools-0.76.tar.gz | tar zxv && \
    cd /package/admin/daemontools-0.76 && \
    echo 'gcc -O2 -Wimplicit -Wunused -Wcomment -Wchar-subscripts -Wuninitialized -Wshadow -Wcast-qual -Wcast-align -Wwrite-strings --include /usr/include/errno.h' > src/conf-cc && \
    package/compile && package/upgrade && mkdir -p /service && chmod 1755 /service && \
  yum remove -y gcc make binutils cpp glibc-devel glibc-headers kernel-headers libgomp libmpc mpfr && \
  yum clean all
ADD setup /package

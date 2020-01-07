FROM debian:stable-slim as glibc-base

ARG GLIBC_VERSION=2.28
ARG GLIBC_PREFIX=/usr/glibc
ENV GLIBC_INSTALL_PATH=/root/glibc

RUN apt-get update && apt-get install -y \
  curl build-essential gawk bison python3 texinfo gettext \
  && rm -rf /var/cache/apt /var/lib/apt \
  && \
  cd /root && \
  curl -SL http://ftp.gnu.org/gnu/glibc/glibc-${GLIBC_VERSION}.tar.gz | tar xzf - \
  && \
  mkdir -p /root/build && cd /root/build && \
  ../glibc-${GLIBC_VERSION}/configure \
    --prefix=${GLIBC_PREFIX} \
    --libdir="${GLIBC_PREFIX}/lib" \
    --libexecdir="${GLIBC_PREFIX}/lib" \
    --enable-multi-arch \
    --enable-stack-protector=strong \
  && \
  make -j`nproc` && make DESTDIR=${GLIBC_INSTALL_PATH} install && \
  cd /root && rm -rf build glibc-${GLIBC_VERSION} && \
  cd ${GLIBC_INSTALL_PATH}${GLIBC_PREFIX} && \
  ( strip bin/* sbin/* lib/* || true )

RUN echo "/usr/local/lib" > ${GLIBC_INSTALL_PATH}${GLIBC_PREFIX}/etc/ld.so.conf && \
  echo "${GLIBC_PREFIX}/lib" >> ${GLIBC_INSTALL_PATH}${GLIBC_PREFIX}/etc/ld.so.conf && \
  echo "/usr/lib" >> ${GLIBC_INSTALL_PATH}${GLIBC_PREFIX}/etc/ld.so.conf && \
  echo "/lib" >> ${GLIBC_INSTALL_PATH}${GLIBC_PREFIX}/etc/ld.so.conf && \
  \
  cd ${GLIBC_INSTALL_PATH}${GLIBC_PREFIX} && \
  rm -rf etc/rpc var include share bin/* sbin/[^l]*  \
	lib/*.o lib/*.a lib/audit lib/gconv lib/getconf

FROM alpine:3.8 as alpine-glibx

ARG GLIBC_PREFIX=/usr/glibc

ENV  LANG=en_US.UTF-8 \
     LANGUAGE=en_US:en
#	 LC_ALL=en_US.UTF-8

COPY --from=glibc-base /root/glibc/ /

RUN ln -s ${GLIBC_PREFIX}/lib/ld-linux-*.so.* /lib && \
  ln -s ${GLIBC_PREFIX}/etc/ld.so.cache /etc && \
  if [ `uname -m` = "x86_64" ]; then ln -s /lib /lib64; fi && \
  ${GLIBC_PREFIX}/sbin/ldconfig

FROM ubuntu:18.04

ENV DEBCONF_NOWARNINGS yes
ENV NAME python
ENV VERSION 3.7.4
ENV ARCHIVE Python-${VERSION}.tgz
ENV SRCDIR /usr/src/${NAME}
ENV BINDIR /usr/local/bin
ENV DOWNLOAD_URL https://www.python.org/ftp/python/${VERSION}/${ARCHIVE}
ENV DOWNLOAD_MD5 68111671e5b2db4aef7b9ab01bf0f9be
ENV DEBIAN_FRONTEND=noninteractive

RUN buildDeps='build-essential libreadline-gplv2-dev libncursesw5-dev libssl-dev libsqlite3-dev tk-dev libgdbm-dev libc6-dev libbz2-dev libffi-dev zlib1g-dev curl ca-certificates' \
  && set -x \
  && majar_version=`echo $VERSION | cut -d '.' -f 1` \
  && apt-get update && apt-get install -y $buildDeps --no-install-recommends \
  && rm -rf /var/lib/apt/lists/* \
  && mkdir -p ${SRCDIR} \
  && curl -sSL "$DOWNLOAD_URL" -o ${ARCHIVE} \
  && echo "$DOWNLOAD_MD5 *${ARCHIVE}" | md5sum -c - \
  && tar xzf ${ARCHIVE} -C ${SRCDIR} --strip-components=1 \
  && rm ${ARCHIVE} \
  && cd ${SRCDIR} \
  && ./configure --enable-optimizations \
  && make install \
  && cd ${BINDIR} \
  && ln -s ${BINDIR}/${NAME}${majar_version} ${NAME} \
  && ln -s ${BINDIR}/pip${majar_version} pip \
  && rm -fr ${SRCDIR} \
  && apt-get purge -y --auto-remove $buildDeps

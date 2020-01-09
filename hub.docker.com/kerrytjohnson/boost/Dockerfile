FROM centos:centos7.5.1804

ENV BOOST_VER=1.71.0
ENV BOOST_VER_U=1_71_0
ENV BOOST_URL=https://dl.bintray.com/boostorg/release
ENV BOOST_SRC_FILE=boost_${BOOST_VER_U}.tar.gz
ENV BOOST_ARTIFACT=boost-${BOOST_VER}.tgz

RUN yum -y -q install   gcc-c++         \
                        make            \
                        python2-devel   \
                        wget

VOLUME /var/tmp

WORKDIR /tmp
RUN wget --quiet ${BOOST_URL}/${BOOST_VER}/source/${BOOST_SRC_FILE} \
    && tar xzf ${BOOST_SRC_FILE}

# Deliberately create a new layer for the build step
WORKDIR /tmp/boost_${BOOST_VER_U}
RUN ./bootstrap.sh  \
    && ./b2

# Deliberately create a new layer for 'installation' and 'packaging'
RUN rm -rf /usr/local/*     \
    && ./b2 install         \
    && rm -rf /tmp/*

WORKDIR /usr/local
RUN tar czf /tmp/${BOOST_ARTIFACT} ./include ./lib

CMD cp /tmp/${BOOST_ARTIFACT} /var/tmp/

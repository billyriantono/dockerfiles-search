FROM alljoynsville/android-base

ENV IOTIVITY_VERSION 1.2-rel

RUN apt-get -yqq update && apt-get install -yqq \
      git-core scons bzip2 \
      && apt-get clean && rm -rf /var/lib/apt/lists/*

#RUN git clone https://gerrit.iotivity.org/gerrit/p/iotivity.git --branch ${IOTIVITY_VERSION} && /
#    cd iotivity && \
#      git clone https://github.com/01org/tinycbor.git extlibs/tinycbor/tinycbor && \
#      git clone https://github.com/ARMmbed/mbedtls.git extlibs/mbedtls/mbedtls
      



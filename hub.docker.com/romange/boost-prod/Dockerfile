ARG DIST=18
FROM romange/boost-builder:$DIST as boost_libs

FROM ubuntu:${DIST}.04
ARG DIST
COPY install.sh /tmp/
RUN /tmp/install.sh ${DIST}

COPY --from=boost_libs /opt/boost/lib/*.so.* /usr/local/lib/
WORKDIR /app

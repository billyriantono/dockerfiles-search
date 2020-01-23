FROM goodrainapps/alpine:3.4

ENV GOST_VER=2.4
ENV PATH=$PATH:/opt/goodrain/gost
ENV PACKAGE_URL=https:/pkg.goodrain.com

RUN mkdir -pv /opt/goodrain \
    && curl -s ${PACKAGE_URL}/apps/gost/gost_${GOST_VER}_linux_amd64.tar.gz | tar -xz -C /opt/goodrain \
    && ln -s /opt/goodrain/gost_${GOST_VER}_linux_amd64 /opt/goodrain/gost


COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT [ "/docker-entrypoint.sh" ]

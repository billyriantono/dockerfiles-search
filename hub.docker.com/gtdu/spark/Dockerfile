FROM docker as downloader
ARG version=3.0.0-preview
WORKDIR /root
RUN wget -q http://archive.apache.org/dist/spark/spark-${version}/spark-${version}-bin-hadoop2.7.tgz 
RUN mkdir spark && tar xf spark-${version}-bin-hadoop2.7.tgz  --directory ~/spark --strip-components=1

FROM openjdk:8-alpine

RUN set -ex && \
    apk upgrade --no-cache && \
    apk add --no-cache bash tini libc6-compat linux-pam nss && \
    mkdir -p /opt/spark && \
    mkdir -p /opt/spark/work-dir && \
    touch /opt/spark/RELEASE && \
    rm /bin/sh && \
    ln -sv /bin/bash /bin/sh && \
    echo "auth required pam_wheel.so use_uid" >> /etc/pam.d/su && \
    chgrp root /etc/passwd && chmod ug+rw /etc/passwd

COPY --from=downloader /root/spark/jars /opt/spark/jars
COPY --from=downloader /root/spark/bin /opt/spark/bin
COPY --from=downloader /root/spark/sbin /opt/spark/sbin
COPY --from=downloader /root/spark/kubernetes/dockerfiles/spark/entrypoint.sh /opt/
COPY --from=downloader /root/spark/examples /opt/spark/examples
COPY --from=downloader /root/spark/kubernetes/tests /opt/spark/tests
COPY --from=downloader /root/spark/data /opt/spark/data

ENV SPARK_HOME /opt/spark

WORKDIR /opt/spark/work-dir

ENTRYPOINT [ "/opt/entrypoint.sh" ]
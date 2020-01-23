FROM openjdk:8-alpine3.8
## Spark standalone mode Dockerfile

ARG version
ARG release
LABEL com.alexsavio.spark.vendor=alexsav.io \
      com.alexsavio.spark.version=$version \
      com.alexsavio.spark.release=$release

ENV SPARK_HOME=/spark \
    SPARK_PGP_KEYS="A864F0C3E5262F9A229B85D07B165D2A15E06093 3E1CBD0F0533D602E80C6E986B32946082667DC1 9555DAB91FFA8A15D0925B87B1A91F0000799F7E"

RUN adduser -Ds /bin/bash -h ${SPARK_HOME} spark && \
    apk add --no-cache bash tini libc6-compat linux-pam krb5 krb5-libs && \
# download dist
    apk add --virtual .deps --no-cache curl tar gnupg && \
    cd /tmp && export GNUPGHOME=/tmp && \
    file=spark-${version}-bin-hadoop2.7.tgz && \
    curl --remote-name-all -w "%{url_effective} fetched\n" -sSL \
        https://archive.apache.org/dist/spark/spark-${version}/{${file},${file}.asc} && \
#    gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys ${SPARK_PGP_KEYS} && \
#    gpg --batch --verify ${file}.asc ${file} && \
# create spark directories
    mkdir -p ${SPARK_HOME}/work ${SPARK_HOME}/conf && chown spark:spark ${SPARK_HOME}/work && \
    tar -xzf ${file} --no-same-owner --strip-components 1 && \
    mv bin data examples jars sbin ${SPARK_HOME} && \
# cleanup
    apk --no-cache del .deps && ls -A | xargs rm -rf

COPY entrypoint.sh /
COPY spark-env.sh ${SPARK_HOME}/conf/

WORKDIR ${SPARK_HOME}/work
ENTRYPOINT [ "/entrypoint.sh" ]

# Specify the User that the actual main process will run as
USER spark:spark
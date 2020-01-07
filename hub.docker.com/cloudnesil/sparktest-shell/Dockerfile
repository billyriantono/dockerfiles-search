FROM cloudnesil/sparktest-oracle-jdk

RUN opkg-install bash libstdcpp zlib

ENV SPARK_BINARY_RELEASE 1.3.0-bin-hadoop2.4

RUN curl \
  --silent \
  --location \
  --retry 3 \
  --insecure \
  https://d3kbcqa49mib13.cloudfront.net/spark-$SPARK_BINARY_RELEASE.tgz \
    | gunzip \
    | tar x -C /usr/ \
  && ln -s /usr/spark-$SPARK_BINARY_RELEASE /usr/spark



## Currently we need to tweak nsswitch.conf(5), mainly due to zettio/weave#68
RUN sed 's/^\(hosts:[\ ]*\)\(files\)\ \(dns\)$/\1\3 \2/' -i /etc/nsswitch.conf

ENV SPARK_HOME /usr/spark-$SPARK_BINARY_RELEASE
ENV PATH $PATH:$SPARK_HOME/bin:/usr/python/bin/

ENTRYPOINT [ "spark-shell" ]

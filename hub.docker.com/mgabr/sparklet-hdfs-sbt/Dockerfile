#
# Spark and Hadoop Standalone Container with sbt
# Apache Spark 2.4.4, Hadoop 2.6, sbt 1.2.8
#
# Runs a small Spark standalone cluster and a pseudo distributed Hadoop cluster in a container
# Suitable for building test/development containers for Spark apps interacting with HDFS
# Provides sbt for building and testing apps directly in the container
#
# Takes some time to start HDFS, in scripts you can use sleep 30
#
# Usage:
# $ docker build -t mgabr/sparklet-hdfs-sbt:2.4.4 -f Dockerfile-sbt .
# $ docker run -p 8080:8080 -p 50070:50070 -it mgabr/sparklet-hdfs-sbt:2.4.4

FROM mgabr/sparklet-hdfs:2.4.4
LABEL author="Markus Gabriel"

RUN \
  curl -fsL https://github.com/sbt/sbt/releases/download/v1.2.8/sbt-1.2.8.tgz > sbt.tgz && \
  # extract sbt
  tar -xzf sbt.tgz && \
  # cleanup sbt tarball
  rm sbt.tgz

ENV PATH /opt/sbt/bin:$PATH

ENTRYPOINT [ "/init" ]

CMD ["sbt"]
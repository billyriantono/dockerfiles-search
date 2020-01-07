########################################################################
# Dockerfile for Spark 1.4.0 with Hadoop 2.7.0 on JDK 8
#
#                    ##        .
#              ## ## ##       ==
#           ## ## ## ##      ===
#       /""""""""""""""""\___/ ===
#  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
#       \______ o          __/
#         \    \        __/
#          \____\______/
#
# Component:    Spark 1.4
# Author:       pjan vandaele <pjan@pjan.io>
# Scm url:      https://github.com/pjan/docker-spark
# License:      MIT
########################################################################

# pull base image
FROM docxs/hadoop:2.7

# maintainer details
MAINTAINER \
  pjan vandaele "pjan@pjan.io"

# set environment variables
ENV SPARK_VERSION_MAJOR  1
ENV SPARK_VERSION_MINOR  4
ENV SPARK_VERSION_BUILD  0
ENV SPARK_VERSION ${SPARK_VERSION_MAJOR}.${SPARK_VERSION_MINOR}.${SPARK_VERSION_BUILD}
ENV SPARK_HOME /opt/spark

# Install Spark
RUN curl -jksSL http://d3kbcqa49mib13.cloudfront.net/spark-1.4.0-bin-hadoop2.6.tgz | tar -xzf - -C /opt \
 && ln -s /opt/spark-1.4.0-bin-hadoop2.6 $SPARK_HOME \
 && mkdir -p $SPARK_HOME/yarn-remote-client \
 && mv /bin/bootstrap /bin/bootstrap-hadoop

# set additional variables
ENV YARN_CONF_DIR $HADOOP_PREFIX/etc/hadoop
ENV PATH $PATH:$SPARK_HOME/bin

# Add configuration files
ADD config /src/config

# Add the binary files
ADD bin /bin/

# expose the relevant ports
EXPOSE \
  7077 8080

# Run bootstrap on container launch
ENTRYPOINT \
  ["bootstrap"]

# Default command
CMD \
  ["-bash"]

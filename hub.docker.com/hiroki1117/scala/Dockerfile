FROM openjdk:8

ENV INSTALL_DIR=/usr/local

ENV SCALA_VERSION=2.13.0

ENV SCALA_HOME=$INSTALL_DIR/scala-$SCALA_VERSION

ENV PATH=$SCALA_HOME/bin:$PATH

RUN apt-get update \
 && wget https://downloads.lightbend.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz -P $INSTALL_DIR \
 && tar -xvzf $INSTALL_DIR/scala-$SCALA_VERSION.tgz -C $INSTALL_DIR

ENTRYPOINT scala
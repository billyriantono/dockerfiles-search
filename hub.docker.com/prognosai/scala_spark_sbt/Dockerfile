# Pull base image
FROM circleci/java:8
USER circleci
ARG SCALA_VERSION
ARG SBT_VERSION

ENV SCALA_VERSION ${SCALA_VERSION:-2.12.5}
ENV SBT_VERSION ${SBT_VERSION:-1.1.2}
ENV SPARK_VERSION ${SPARK_VERSION:-2.3.0}

LABEL prognos.ai="Prognos AI" \
      author="ashah@prognos.ai" \
      maintainer="sectechops@prognos.ai" \
      version="2.12.5_2.3.0_1.1.2" \
      description="Image with scala, spark and sbt"


RUN \
  echo "building docker image for scala $SCALA_VERSION sbt $SBT_VERSION"

RUN \
  echo "Downloading and setting up Scala $SCALA_VERSION" && \
  cd && wget -q http://downloads.typesafe.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz && \
  tar -xzf scala-$SCALA_VERSION.tgz && \
  sudo ln -s /home/circleci/scala-$SCALA_VERSION/bin/* /usr/local/bin/

RUN \
  echo "Downloading and setting up SBT ${SBT_VERSION}" && \
  cd && wget -q https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz && \
  tar -xzf sbt-$SBT_VERSION.tgz && \
  sudo ln -s /home/circleci/sbt/bin/* /usr/local/bin/

RUN \
  echo "Downloading and setting up Spark $SPARK_VERSION" && \
  cd && wget -q http://apache.claz.org/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-hadoop2.7.tgz && \
  tar -xzf spark-$SPARK_VERSION-bin-hadoop2.7.tgz && \
  sudo ln -s /home/circleci/spark-$SPARK_VERSION-bin-hadoop2.7/bin/* /usr/local/bin/ && \
  sudo mkdir -p /usr/local/assembly/target/scala-2.12 && \
  sudo ln -s /home/circleci/spark-$SPARK_VERSION-bin-hadoop2.7/jars /usr/local/assembly/target/scala-2.12/jars

CMD ["/bin/sh"]
FROM python:3.5.6-stretch

MAINTAINER  Ludwig Prager <ludwig.prager@celp.de>

RUN apt update && apt -y install \
	wget \
	openjdk-8-jdk \
	vim less

RUN rm -rf /var/lib/apt/lists/*

ENV HADOOP 2.7
ENV SPARK 2.2.0
ENV SBT 0.13.13

ENV SPARK_ARCHIVE spark-${SPARK}-bin-hadoop${HADOOP}.tgz
RUN wget https://archive.apache.org/dist/spark/spark-${SPARK}/spark-${SPARK}-bin-hadoop${HADOOP}.tgz
RUN tar -zxf ${SPARK_ARCHIVE}
RUN rm ${SPARK_ARCHIVE}

RUN echo "SPARK_HOME=/spark-${SPARK}-bin-hadoop${HADOOP}/" >> ~/.bashrc
RUN echo "PATH=$PATH:/spark-${SPARK}-bin-hadoop${HADOOP}/bin" >> ~/.bashrc

# sbt
RUN wget https://dl.bintray.com/sbt/debian/sbt-${SBT}.deb
RUN dpkg -i sbt-${SBT}.deb
RUN rm sbt-${SBT}.deb
RUN sbt sbtVersion

# test app
WORKDIR /SimpleApp/
RUN mkdir -p src/main/scala/
COPY SimpleApp/SimpleApp.scala src/main/scala/
COPY SimpleApp/build.sbt .

WORKDIR /SimpleApp/
RUN cp /spark-${SPARK}-bin-hadoop2.7/README.md .
RUN sbt package
RUN /spark-${SPARK}-bin-hadoop${HADOOP}/bin/spark-submit \
	--class "SimpleApp" \
	--master local[4] \
	target/scala-2.11/simple-project_2.11-1.0.jar

WORKDIR /my_project/

RUN ["/bin/bash"]

FROM java:8-jdk-alpine

ENV DAEMON_RUN=true
ENV SPARK_VERSION=2.4.4
ENV HADOOP_VERSION=2.7
ENV SCALA_VERSION=2.13.1
ENV SCALA_HOME=/usr/share/scala

#Install Scala
RUN apk add --no-cache wget ca-certificates tar gzip bash curl jq && \
	cd "/tmp" && \
	wget --no-verbose "https://downloads.lightbend.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz" && \
	tar xzf "scala-${SCALA_VERSION}.tgz" && \
	mkdir "${SCALA_HOME}" && \
	rm "/tmp/scala-${SCALA_VERSION}/bin/"*.bat && \
	mv "/tmp/scala-${SCALA_VERSION}/bin" "/tmp/scala-${SCALA_VERSION}/lib" "${SCALA_HOME}" && \
	ln -s "${SCALA_HOME}/bin"* "/usr/bin/" && \
	rm -rf "/tmp/"*
	
#Install SBT (Scala Build Tool)
RUN export PATH="/usr/local/sbt/bin:$PATH" && \ 
	apk update && \
	apk add ca-certificates wget tar gzip && \
	mkdir -p "/usr/local/sbt" && \
	wget --no-check-certificate --no-verbose "https://piccolo.link/sbt-1.3.2.tgz" && \
	tar xzf "sbt-1.3.2.tgz" -C /usr/local/sbt --strip-components=1 && \
	sbt sbtVersion	
	
#Install Python
RUN apk add --no-cache python3 && \
	ln -s /usr/bin/python3 /usr/bin/python && \
    ln -s /usr/bin/pip3 /usr/bin/pip

#Install Spark
RUN wget --no-verbose http://apache.mirror.iphh.net/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && tar -xvzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} spark \
      && rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz
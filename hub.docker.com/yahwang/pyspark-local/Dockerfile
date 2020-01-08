FROM python:3.7-slim-stretch

ARG SPARK_VERSION=2.4.4
ARG HADOOP_VERSION=2.7

ARG PYTHON_DEPS=" \ 
        jupyterlab==1.2.3 \
        pandas==0.25.3 \
        numpy==1.17.4 \
        pyarrow==0.14.1 \
        "

ENV LANG=en_US.UTF-8 \
    JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 \
    SPARK_HOME=/usr/local/spark \
    PATH="/usr/local/spark/bin:$PATH" \
    PYTHONHASHSEED=0 \
    PYTHONPATH="/usr/local/spark/python:/usr/local/spark/python/lib/py4j-0.10.7-src.zip"
    
RUN apt-get update \
 && apt-get install -y locales \
 && localedef -f UTF-8 -i en_US en_US.UTF-8 \
 && mkdir -p /usr/share/man/man1 \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
        wget \
        ca-certificates \
        gnupg \
        openjdk-8-jre-headless \
 && apt-get remove -yqq \
    gnupg \
 && apt-get autoremove -yqq --purge \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -q http://apache.mirror.cdnetworks.com/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
 && tar xzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz -C /usr/local \
 && mv /usr/local/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} /usr/local/spark \
 && rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
 && wget -q http://central.maven.org/maven2/com/amazonaws/aws-java-sdk/1.7.4/aws-java-sdk-1.7.4.jar -P $SPARK_HOME/jars/ \
 && wget -q http://central.maven.org/maven2/org/apache/hadoop/hadoop-aws/2.7.7/hadoop-aws-2.7.7.jar -P $SPARK_HOME/jars/ \
 && cp $SPARK_HOME/conf/spark-defaults.conf.template $SPARK_HOME/conf/spark-defaults.conf \
 && echo "spark.hadoop.fs.s3a.impl=org.apache.hadoop.fs.s3a.S3AFileSystem" >> $SPARK_HOME/conf/spark-defaults.conf \
 && echo "spark.sql.execution.arrow.enabled=true" >> $SPARK_HOME/conf/spark-defaults.conf

RUN pip install --no-cache-dir \
    ${PYTHON_DEPS}

EXPOSE 8888 4040-4042
WORKDIR /home/notebooks
CMD ["jupyter","lab","--ip=0.0.0.0","--NotebookApp.token=''","--allow-root","--no-browser"]


FROM haidong/hadoop
MAINTAINER haidong <383623085@qq.com>

# Set environment variables for program versions
ARG SPARK_VERSION=2.1.1
ENV SPARK_HOME /opt/spark

# Download and extract spark to opt folder
RUN curl -L http://mirror.bit.edu.cn/apache/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop2.7.tgz \    
    | tar -zx -C /opt \
    && ln -s /opt/spark-${SPARK_VERSION}-bin-hadoop2.7 ${SPARK_HOME}

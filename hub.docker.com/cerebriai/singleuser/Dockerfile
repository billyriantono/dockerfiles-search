# Build as jupyterhub/singleuser
# Run with the DockerSpawner in JupyterHub

FROM adoptopenjdk/openjdk8:slim as openjdk
RUN echo "In stage openjdk" \
    && ls -la /opt/java/openjdk

FROM cerebriai/spark as spark
RUN echo "In stage spark" \
    && ls -la /opt/spark

ENV HADOOP_VERSION 3.2.0
FROM cerebriai/hadoop:3.2.0 as hadoop
RUN echo "In stage hadoop" \
    && ls -la /opt/hadoop-$HADOOP_VERSION

#Main Install
FROM jupyter/base-notebook
MAINTAINER Nic Swart <nic@cerebriai.com>

# Java
COPY --from=openjdk /opt/java/openjdk /opt/java/openjdk
ENV JAVA_HOME=/opt/java/openjdk
ENV PATH=$PATH:${JAVA_HOME}/bin
RUN echo "In stage airflow" \
    && java -version

# Spark
#RUN rm -rf /usr/local/spark
COPY --from=spark /opt/spark /opt/spark
COPY --from=spark /dependencies/ /dependencies
ENV SPARK_HOME /opt/spark
ENV PATH=$PATH:${SPARK_HOME}/bin
RUN echo "In stage singeluser jupyter" \
    && spark-submit --version \
    && echo $SPARK_HOME \
    && echo $PATH

ENV HADOOP_VERSION 3.2.0
COPY --from=hadoop /opt/hadoop-$HADOOP_VERSION /opt/hadoop-$HADOOP_VERSION
ENV HADOOP_HOME=/opt/hadoop-$HADOOP_VERSION
ENV HADOOP_PREFIX=/opt/hadoop-$HADOOP_VERSION
ENV HADOOP_CLASSPATH=$HADOOP_CLASSPATH:/opt/hadoop-$HADOOP_VERSION/share/hadoop/tools/lib/*
ENV HADOOP_CONF_DIR=/etc/hadoop
ADD core-site.xml /etc/hadoop/core-site.xml
ADD hdfs-site.xml /etc/hadoop/hdfs-site.xml
ENV HADOOP_OPTIONAL_TOOLS=hadoop-azure
ENV MULTIHOMED_NETWORK=1
ENV PATH=$PATH:$HADOOP_PREFIX/bin

ADD install_jupyterhub.py /tmp/install_jupyterhub.py
#ARG JUPYTERHUB_VERSION=0.9.4
ARG JUPYTERHUB_VERSION=1.0.0
# install pinned jupyterhub and ensure notebook is installed
RUN python3 /tmp/install_jupyterhub.py && \
    python3 -m pip install notebook
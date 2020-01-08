FROM jupyter/datascience-notebook

USER root
ENV HADOOP_VERSION 2.7.7
ENV SPARK_VERSION=2.4.3

ENV TZ=Asia/Shanghai
ENV HADOOP_PREFIX=/opt/hadoop-$HADOOP_VERSION
ENV HADOOP_CONF_DIR=/etc/hadoop
ENV MULTIHOMED_NETWORK=1
ENV USER=root
ENV PATH $HADOOP_PREFIX/bin/:$PATH
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/
ENV HADOOP_URL https://www.apache.org/dist/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz

COPY import.py /
COPY cli /opt/conda/bin/cli
COPY demo.ipynb /home/jovyan/

RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends openjdk-8-jdk net-tools curl netcat gnupg iputils-ping \ 
           fonts-wqy-microhei ttf-wqy-zenhei && fc-cache -fv && \ 
    curl -O https://dist.apache.org/repos/dist/release/hadoop/common/KEYS && \
    gpg --import KEYS && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf KEYS && \
    set -x \
    && curl -fSL "$HADOOP_URL" -o /tmp/hadoop.tar.gz \
    && curl -fSL "$HADOOP_URL.asc" -o /tmp/hadoop.tar.gz.asc \
    && gpg --verify /tmp/hadoop.tar.gz.asc \
    && tar -xvf /tmp/hadoop.tar.gz -C /opt/ \
    && rm /tmp/hadoop.tar.gz* && \
    ln -s /opt/hadoop-$HADOOP_VERSION/etc/hadoop /etc/hadoop && \
    mkdir /opt/hadoop-$HADOOP_VERSION/logs && \
    mkdir /hadoop-data && \
    chmod +x /opt/conda/bin/cli && \
    pip install --no-cache-dir svgwrite sklearn plotly bokeh jupytext chartify cufflinks altair vega_datasets vega folium pyspark==$SPARK_VERSION pandas-profiling RISE && \
    jupyter lab build && \
    rm -rf /home/jovyan/.cache/matplotlib
    
USER $NB_UID
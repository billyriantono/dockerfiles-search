FROM dataismus/jupyspark

# EXPOSE 22

# USER root
# # SSH config and launch
# COPY ssh_config /etc/ssh/ssh_config
# COPY ssh_config /root/.ssh/config
# RUN chmod 600 /root/.ssh/config /etc/ssh/ssh_config && \
#     chown root:root /root/.ssh/config /etc/ssh/ssh_config
# RUN ssh-keygen -t rsa -P '' -f /root/.ssh/id_rsa && \
#     cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys && \
#     chmod 0600 ~/.ssh/authorized_keys && \
#     service ssh start

# HADOOP & YARN config
ENV HADOOP_HOME /hadoop
ENV HADOOP_CONF_DIR ${HADOOP_HOME}/etc/hadoop
ENV HADOOP_HDFS_HOME ${HADOOP_HOME}
ENV YARN_HOME ${HADOOP_HOME}

COPY core-site.xml ${HADOOP_CONF_DIR}/core-site.xml
COPY yarn-site.xml ${HADOOP_CONF_DIR}/yarn-site.xml
COPY hdfs-site.xml ${HADOOP_CONF_DIR}/hdfs-site.xml
# spark-submit --master yarn --class --deploy-mode client \
# org.apache.spark.examples.SparkPi $SPARK_HOME/examples/jars/spark-examples_2.11-${APACHE_SPARK_VERSION}.jar 100

USER $NB_UID
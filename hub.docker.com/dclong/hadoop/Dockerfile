FROM dclong/scala

ARG hadoop=hadoop-2.8.2
RUN wget http://apache.claz.org/hadoop/common/${hadoop}/${hadoop}.tar.gz -O /hadoop.tar.gz \
    && tar -zxf /hadoop.tar.gz -C /opt/ \
    && rm /hadoop.tar.gz \
    && /opt/${hadoop}/bin/hadoop fs -mkdir -p /user/hive/warehouse \
    && /opt/${hadoop}/bin/hadoop fs -mkdir -p /tmp \
    && /opt/${hadoop}/bin/hadoop fs -chmod g+w /user/hive/warehouse \
    && /opt/${hadoop}/bin/hadoop fs -chmod g+w /tmp

ENV HADOOP_HOME=/opt/${hadoop} \
    HADOOP_CONF_DIR=/opt/${hadoop}/etc/hadoop \
    HADOOP_MAPRED_HOME=/opt/${hadoop} \
    HADOOP_COMMON_HOME=/opt/${hadoop} \
    HADOOP_HDFS_HOME=/opt/${hadoop} \
    HADOOP_COMMON_LIB_NATIVE_DIR=${HADOOP_HOME}/lib/native \
    HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib" \
    HADOOP_PID_DIR=$HADOOP_HOME/hadoop2_data/hdfs/pid \
    YARN_HOME=/opt/${hadoop} \
    PATH=$PATH:$HADOOP_HOME/bin

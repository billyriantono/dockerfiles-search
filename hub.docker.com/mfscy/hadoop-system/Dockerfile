FROM opensuse/tumbleweed

LABEL author="Fadhil Yori Hibatullah <fadhil4812@gmail.com>" \
    description="Hadoop 3.0.0 Base Docker Image"

COPY repo/opensuse/cloudera-cdh.repo /opt/.
RUN zypper addrepo -f -r /opt/cloudera-cdh.repo \
    && zypper --gpg-auto-import-keys ref \
    && zypper in -y hadoop \
    python-setuptools \
    java-1_8_0-openjdk-devel \
    hadoop-hdfs-namenode \
    hadoop-client \
    wget \
    nano \
    && zypper clean
ENV JAVA_HOME /usr/lib64/jvm/jre-1.8.0-openjdk
ENV HADOOP_HOME /usr/lib/hadoop
ENV HADOOP_CONF_DIR /etc/hadoop/conf
ENV HADOOP_COMMON_HOME /usr/lib/hadoop
ENV HADOOP_HDFS_HOME /usr/lib/hadoop-hdfs
ENV HADOOP_YARN_HOME /usr/lib/hadoop-yarn
ENV HADOOP_MAPRED_HOME /usr/lib/hadoop-mapreduce
CMD [ "hadoop", "version" ]
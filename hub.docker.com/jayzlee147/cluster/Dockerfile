FROM ubuntu

LABEL author="jayzlee"

COPY entrypoint.sh config/* /root/
RUN \
apt update && \
apt-get install openssh-server wget openjdk-8-jdk -y && \
ssh-keygen -q -N "" -t rsa -f /root/.ssh/id_rsa && cat /root/.ssh/id_rsa.pub >> /root/.ssh/authorized_keys && \
echo "    StrictHostKeyChecking no\n    UserKnownHostsFile /dev/null" >> /etc/ssh/ssh_config && \
wget -O /opt/hadoop.tar.gz  https://www-us.apache.org/dist/hadoop/common/hadoop-3.1.1/hadoop-3.1.1.tar.gz && \
tar -zxvf /opt/hadoop.tar.gz -C /opt && mv /opt/hadoop-3.1.1 /opt/hadoop && rm /opt/hadoop.tar.gz && rm -rf /opt/hadoop/share/doc/hadoop && \
echo "JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64" >> /opt/hadoop/etc/hadoop/hadoop-env.sh && \
mv -f /root/*.xml /root/workers /opt/hadoop/etc/hadoop/ && \
mv -f /root/s*.sh /opt/hadoop/sbin/ && \
chmod a+x /root/entrypoint.sh && chmod -R a+x /opt/hadoop && chown -R root:root /opt/hadoop

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 HADOOP_HOME=/opt/hadoop

WORKDIR /opt/hadoop

ENTRYPOINT ["/root/entrypoint.sh"]
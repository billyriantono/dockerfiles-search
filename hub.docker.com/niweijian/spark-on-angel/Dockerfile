FROM niweijian/angel

MAINTAINER weijian ni <weijianni@gmail.com>

COPY sources.list /etc/apt

WORKDIR /src

RUN git clone https://github.com/Angel-ML/sona.git

RUN wget http://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-2.4.4/spark-2.4.4-bin-hadoop2.7.tgz
RUN tar xvf spark-2.4.4-bin-hadoop2.7.tgz


COPY capacity-scheduler.xml /usr/local/hadoop/etc/hadoop/
RUN cd /src/sona && git checkout -b branch-0.1.0 origin/branch-0.1.0
COPY pom.xml /src/sona
RUN cd /src/sona && mvn clean package -Dmaven.test.skip=true

COPY spark-on-angel-env.sh /src/sona/dist/target/sona-0.1.0-bin/bin
COPY lr.json /src/sona/dist/target/sona-0.1.0-bin/bin
COPY yarn-site.xml /usr/local/hadoop/etc/hadoop/yarn-site.xml
COPY SONA-example /src/sona/dist/target/sona-0.1.0-bin/bin
RUN cd /src/angel/dist/target/angel-3.0.1-bin/lib/ && cp angel-ps-core-3.0.1.jar hadoop-mapreduce-client-app-3.1.0.jar hadoop-mapreduce-client-common-3.1.0.jar hadoop-mapreduce-client-core-3.1.0.jar hadoop-mapreduce-client-hs-3.1.0.jar	hadoop-mapreduce-client-hs-plugins-3.1.0.jar hadoop-mapreduce-client-jobclient-3.1.0.jar hadoop-mapreduce-client-shuffle-3.1.0.jar jackson-annotations-2.6.5.jar jackson-core-asl-1.9.13.jar jackson-jaxrs-1.9.13.jar jackson-mapper-asl-1.9.13.jar jackson-xc-1.9.13.jar angel-format-0.1.1.jar angel-mlcore-0.1.2.jar angel-ps-mllib-3.0.1.jar angel-ps-psf-3.0.1.jar angel-math-0.1.1.jar angel-ps-graph-3.0.1.jar angel-ps-tools-3.0.1.jar /src/sona/dist/target/sona-0.1.0-bin/lib/
RUN echo "export JAVA_HOME=/usr" >> /root/.bashrc && \
    echo "export HADOOP_HOME=/usr/local/hadoop" >> /root/.bashrc && \
	echo "export PATH=\$PATH:\$HADOOP_HOME/bin" >> /root/.bashrc && \
    echo "bash /src/start.sh" >> /root/.bashrc
COPY line-example /src/sona/dist/target/sona-0.1.0-bin/bin
COPY louvain-example /src/sona/dist/target/sona-0.1.0-bin/bin

RUN echo 'root:123456' |chpasswd  && \
	sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
	sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

EXPOSE 22
FROM ikuai/hadoop

MAINTAINER Dylan <bbcheng@ikuai8.com>

# Version
ENV SPARK_VERSION=2.2.1

# Set home
ENV SPARK_HOME=/usr/local/spark-$SPARK_VERSION

# Install dependencies
RUN apt-get update \
	&& DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends python python3 \
	&& apt-get autoremove -y \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

# Install Spark
RUN mkdir -p "${SPARK_HOME}" \
	&& export ARCHIVE=spark-$SPARK_VERSION-bin-without-hadoop.tgz \
	&& export DOWNLOAD_PATH=apache/spark/spark-$SPARK_VERSION/$ARCHIVE \
	&& curl -sSL http://download.nextag.com/$DOWNLOAD_PATH | tar -xz -C $SPARK_HOME --strip-components 1 \
	&& rm -rf $ARCHIVE

COPY spark-env.sh $SPARK_HOME/conf/spark-env.sh
ENV PATH=$PATH:$SPARK_HOME/bin
ENV LD_LIBRARY_PATH=$HADOOP_HOME/lib/native/:$LD_LIBRARY_PATH

# Copy start script
COPY start-spark /opt/util/bin/start-spark

# Fix environment for other users
RUN chmod +x /opt/util/bin/start-spark \
	&& echo "export SPARK_HOME=$SPARK_HOME" >> /etc/bash.bashrc \
	&& echo 'export PATH=$PATH:$SPARK_HOME/bin'>> /etc/bash.bashrc

# Add deprecated commands
RUN echo '#!/usr/bin/env bash' > /usr/bin/master \
	&& echo 'start-spark master' >> /usr/bin/master \
	&& chmod +x /usr/bin/master \
	&& echo '#!/usr/bin/env bash' > /usr/bin/worker \
	&& echo 'start-spark worker $1' >> /usr/bin/worker \
	&& chmod +x /usr/bin/worker

# Ports
EXPOSE 6066 7077 8080 8081
	
CMD ["/usr/sbin/sshd", "-D"]
FROM factual/docker-cdh5-base

ENV HADOOP_CONF_DIR=/etc/hadoop/conf

RUN apt-add-repository ppa:brightbox/ruby-ng \
  && add-apt-repository "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main" \
  && curl https://www.postgresql.org/media/keys/ACCC4CF8.asc | apt-key add - \
  && apt-get update && apt-get install -y --no-install-recommends \
    git-core sudo build-essential unzip zlib1g-dev \
    liblzo2-dev libcurl4-gnutls-dev libncurses5-dev libpq-dev \
    vim emacs \
    ruby2.4 ruby2.4-dev uuid-runtime \
    postgresql-client-9.6 \
    openjdk-8-jdk-headless ant \
    nodejs npm \
    python3 python3-dev \
    ldap-utils libpam-ldap libnss-ldap nslcd \
    s3cmd awscli \
    jq \
    manpages manpages-dev man-db \
  && update-ca-certificates -f \
  && rm -rf /var/lib/apt/lists/*


RUN curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py \
  && python3 get-pip.py \
  && rm get-pip.py \
  && pip install --no-cache-dir \
    matplotlib \
    numpy \
    pandas \
    pipenv \
    scikit-learn \
    scipy \
  && gem install bundler --no-rdoc --no-ri

#maven
ENV MAVEN_VERSION=3.6.3
ENV MAVEN_PATH=/opt/apache-maven
RUN mkdir -p $MAVEN_PATH \
  && curl -fsSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
    | tar xz --strip-components=1 -C $MAVEN_PATH \
  && ln -s $MAVEN_PATH/bin/mvn /usr/bin/mvn

#lein
ARG LEIN_ROOT=true
RUN curl -fsSL https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein -o /bin/lein \
  && chmod 755 /bin/lein \
  && lein --version

#Drake
RUN curl -fsSL https://raw.githubusercontent.com/Factual/drake/master/bin/drake -o /bin/drake \
  && chmod 755 /bin/drake

#Spark
# When updating. ensure /apps/spark/$SPARK_VERSION is populated
ENV SPARK_VERSION=2.4.4
ENV SPARK_SCALA_HADOOP=without-hadoop-scala-2.12
ENV SPARK_HOME=/opt/spark

RUN mkdir -p $SPARK_HOME \
  && curl -fsSL http://archive.apache.org/dist/spark/spark-$SPARK_VERSION/spark-$SPARK_VERSION-bin-$SPARK_SCALA_HADOOP.tgz \
    | tar xz -C /tmp/ \
  && rm -rf $SPARK_HOME && mv /tmp/spark-$SPARK_VERSION-bin-$SPARK_SCALA_HADOOP $SPARK_HOME \
  && mkdir -p /etc/spark/ \
  && ln -s $SPARK_HOME/conf /etc/spark/conf
COPY spark-defaults.conf /etc/spark/conf/
RUN echo "spark.yarn.jars                  hdfs://dev/apps/spark/$SPARK_VERSION/*" >> /etc/spark/conf/spark-defaults.conf
# Necessary to use a without-hadoop spark distribution
RUN echo 'export SPARK_DIST_CLASSPATH=$(hadoop classpath)' >> /etc/spark/conf/spark-env.sh

#hive
ENV HIVE_VERSION=2.3.6
ENV HIVE_HOME=/opt/hive
RUN mkdir -p $HIVE_HOME \
  && curl -fsSL http://archive.apache.org/dist/hive/hive-$HIVE_VERSION/apache-hive-$HIVE_VERSION-bin.tar.gz \
    | tar xz --strip-components=1 -C $HIVE_HOME \
  && mkdir -p /etc/hive/ \
  && ln -s $HIVE_HOME/conf /etc/hive/conf \
  && mv /etc/hive/conf/hive-default.xml.template /etc/hive/conf/hive-default.xml \
  && mv /etc/hive/conf/hive-env.sh.template /etc/hive/conf/hive-env.sh

ENV PATH="$HIVE_HOME/bin:$SPARK_HOME/bin:$PATH"
COPY bootstrap.sh /etc/my_init.d/099_bootstrap
VOLUME /var/lib/docker

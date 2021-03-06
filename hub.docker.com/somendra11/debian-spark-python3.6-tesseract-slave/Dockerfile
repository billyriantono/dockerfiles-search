# VERSION 0.1
# AUTHOR: Somendra Joshi
# DESCRIPTION: Python Spark Docker container

FROM debian:stretch
MAINTAINER somendra11

RUN apt-get update \
 && apt-get install -y locales \
 && dpkg-reconfigure -f noninteractive locales \
 && locale-gen C.UTF-8 \
 && /usr/sbin/update-locale LANG=C.UTF-8 \
 && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
 && locale-gen \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# Users with other locales should set this in their derivative image
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Install python and its packages
RUN echo "deb http://ftp.de.debian.org/debian testing main"  >> /etc/apt/sources.list \
 && echo 'APT::Default-Release "stable";' | tee -a /etc/apt/apt.conf.d/00local \
 && apt-get update \
 && apt-get -t testing install -y python3.6 python3-pip wget \
 && apt-get install -y curl unzip \
 && ln -s /usr/bin/python3.6 /usr/bin/python \
 && ln -s /usr/bin/pip3 /usr/bin/pip \
 && pip install py4j fuzzywuzzy inflect nltk scipy unidecode \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# http://blog.stuart.axelbrooke.com/python-3-on-spark-return-of-the-pythonhashseed
ENV PYTHONHASHSEED 0
ENV PYTHONIOENCODING UTF-8
ENV PIP_DISABLE_PIP_VERSION_CHECK 1

# JAVA
ARG JAVA_MAJOR_VERSION=8
ARG JAVA_UPDATE_VERSION=181
ARG JAVA_BUILD_NUMBER=13
ENV JAVA_HOME /usr/jdk1.${JAVA_MAJOR_VERSION}.0_${JAVA_UPDATE_VERSION}

ENV PATH $PATH:$JAVA_HOME/bin
RUN curl -sL --retry 3 --insecure \
  --header "Cookie: oraclelicense=accept-securebackup-cookie;" \
  "http://download.oracle.com/otn-pub/java/jdk/${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-b${JAVA_BUILD_NUMBER}/96a7b8442fe848ef90c96a2fad6ed6d1/server-jre-${JAVA_MAJOR_VERSION}u${JAVA_UPDATE_VERSION}-linux-x64.tar.gz" \
  | gunzip \
  | tar x -C /usr/ \
  && ln -s $JAVA_HOME /usr/java \
  && rm -rf $JAVA_HOME/man

# HADOOP
ENV HADOOP_VERSION 3.0.0
ENV HADOOP_HOME /usr/hadoop-$HADOOP_VERSION
ENV HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
ENV PATH $PATH:$HADOOP_HOME/bin
RUN curl -sL --retry 3 \
  "http://archive.apache.org/dist/hadoop/common/hadoop-$HADOOP_VERSION/hadoop-$HADOOP_VERSION.tar.gz" \
  | gunzip \
  | tar -x -C /usr/ \
 && rm -rf $HADOOP_HOME/share/doc \
 && chown -R root:root $HADOOP_HOME

# SPARK
ENV SPARK_VERSION 2.3.1
ENV SPARK_PACKAGE spark-${SPARK_VERSION}-bin-without-hadoop
ENV SPARK_HOME /usr/spark-${SPARK_VERSION}
ENV SPARK_DIST_CLASSPATH="$HADOOP_HOME/etc/hadoop/*:$HADOOP_HOME/share/hadoop/common/lib/*:$HADOOP_HOME/share/hadoop/common/*:$HADOOP_HOME/share/hadoop/hdfs/*:$HADOOP_HOME/share/hadoop/hdfs/lib/*:$HADOOP_HOME/share/hadoop/hdfs/*:$HADOOP_HOME/share/hadoop/yarn/lib/*:$HADOOP_HOME/share/hadoop/yarn/*:$HADOOP_HOME/share/hadoop/mapreduce/lib/*:$HADOOP_HOME/share/hadoop/mapreduce/*:$HADOOP_HOME/share/hadoop/tools/lib/*"
ENV PATH $PATH:${SPARK_HOME}/bin
RUN curl -sL --retry 3 \
  "https://www.apache.org/dyn/mirrors/mirrors.cgi?action=download&filename=spark/spark-${SPARK_VERSION}/${SPARK_PACKAGE}.tgz" \
  | gunzip \
  | tar x -C /usr/ \
 && mv /usr/$SPARK_PACKAGE $SPARK_HOME \
 && chown -R root:root $SPARK_HOME

# Installing Tesseract

RUN apt-get --yes update; \
  apt-get --yes install autoconf automake libtool; \
  apt-get --yes install autoconf-archive; \
  apt-get --yes install pkg-config; \
  apt-get --yes install libjpeg-dev; \
  apt-get --yes --allow-downgrades install zlib1g=1:1.2.8.dfsg-5 zlib1g-dev; \
  apt-get --yes --allow-downgrades install libpng16-16=1.6.28-1 libpng-dev; \
  apt-get clean \
  && rm -rf /var/lib/apt/lists/*
  # apt-get --yes --allow-downgrades install libtiff5-dev=4.0.9-1;

RUN cd /tmp/ && \
  wget http://www.leptonica.com/source/leptonica-1.76.0.tar.gz && \
  tar xvzf leptonica-1.76.0.tar.gz && \
  cd leptonica-1.76.0 && \
  ./configure && \
  make && \
  make install && \
  rm -rf /tmp/* && \
  cd /tmp/ && \
  wget https://github.com/tesseract-ocr/tesseract/archive/3.05.01.tar.gz && \
  tar xvzf 3.05.01.tar.gz && \
  cd tesseract-3.05.01 && \
  sed -i '$ d' api/Makefile.am && \
  sed -i '$ d' api/Makefile.am && \
  echo 'tesseract_LDADD += -lrt -llept' >> api/Makefile.am && \
  echo 'endif' >> api/Makefile.am && \
  ./autogen.sh && \
  ./configure --enable-debug && \
  LDFLAGS="-L/usr/local/lib" CFLAGS="-I/usr/local/include" make && \
  make install && \
  ldconfig && \
  rm -rf /tmp/* && \
  wget -O /usr/local/share/tessdata/eng.traineddata https://github.com/tesseract-ocr/tessdata/raw/master/eng.traineddata

# install python packages
RUN pip3 install tesserocr pdf2image python-Levenshtein scikit-learn

WORKDIR $SPARK_HOME

CMD ["bin/spark-class", "org.apache.spark.deploy.master.Master"]
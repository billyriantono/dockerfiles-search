FROM docker.elastic.co/elasticsearch/elasticsearch:5.5.0

ARG ELASTICSEARCH_DIRECTORY=/usr/share/elasticsearch

# https://bitbucket.org/eunjeon/mecab-ko/downloads
ARG MECAB_KO=mecab-0.996-ko-0.9.2
# https://bitbucket.org/eunjeon/mecab-ko-dic/downloads
ARG MECAB_KO_DIC=mecab-ko-dic-2.0.3-20170922
# https://bitbucket.org/eunjeon/mecab-java/downloads
ARG MECAB_JAVA=mecab-java-0.996
# https://bitbucket.org/eunjeon/mecab-ko-lucene-analyzer/issues/9/elasticsearch-analysis-mecab-ko-5500zip
ARG MECAB_KO_LUCENE_ANALYZER=elasticsearch-analysis-mecab-ko-5.5.0.0

###############################################################################
# INSTALLATIONS
###############################################################################
USER root
###############################################################################
# install dependencies
###############################################################################
RUN yum --assumeyes --quiet install gcc
RUN yum --assumeyes --quiet install gcc-c++
RUN yum --assumeyes --quiet install make
RUN yum --assumeyes --quiet install automake
RUN yum --assumeyes --quiet install java-1.8.0-openjdk-devel

###############################################################################
# install mecab-ko
###############################################################################
WORKDIR $ELASTICSEARCH_DIRECTORY
COPY $MECAB_KO.tar.gz $MECAB_KO.tar.gz
RUN tar --extract --gzip --file=$MECAB_KO.tar.gz
WORKDIR $ELASTICSEARCH_DIRECTORY/$MECAB_KO
RUN ./configure
RUN make
RUN make check
RUN make install

###############################################################################
# install mecab-ko-dic
###############################################################################
WORKDIR $ELASTICSEARCH_DIRECTORY
COPY $MECAB_KO_DIC.tar.gz $MECAB_KO_DIC.tar.gz
RUN tar --extract --gzip --file=$MECAB_KO_DIC.tar.gz
WORKDIR $ELASTICSEARCH_DIRECTORY/$MECAB_KO_DIC
RUN ./autogen.sh
RUN ./configure
RUN make
RUN make install
RUN ldconfig

###############################################################################
# install mecab-java
###############################################################################
ENV JAVA_TOOL_OPTIONS -Dfile.encoding=UTF8
ENV LD_LIBRARY_PATH /usr/local/lib
WORKDIR $ELASTICSEARCH_DIRECTORY
COPY $MECAB_JAVA.tar.gz $MECAB_JAVA.tar.gz
RUN tar --extract --gzip --file=$MECAB_JAVA.tar.gz
WORKDIR $ELASTICSEARCH_DIRECTORY/$MECAB_JAVA
RUN sed -i "s/\/home\/parallels\/Programs\/jdk1.7.0_75\/include/\/usr\/lib\/jvm\/java-1.8.0-openjdk\/include/g" ./Makefile
RUN sed -i "s/\-O3/\-O1/g" ./Makefile
RUN make
RUN cp libMeCab.so $LD_LIBRARY_PATH

###############################################################################
# install mecab-ko-lucene-analyzer
###############################################################################
WORKDIR $ELASTICSEARCH_DIRECTORY
COPY $MECAB_KO_LUCENE_ANALYZER.zip $MECAB_KO_LUCENE_ANALYZER.zip
RUN elasticsearch-plugin install file:$(/bin/pwd)/$MECAB_KO_LUCENE_ANALYZER.zip

USER elasticsearch
WORKDIR $ELASTICSEARCH_DIRECTORY

FROM centos

MAINTAINER mypjb/logstash docker maintainer 280417314@qq.com

# log stash download url
ENV LOGSTASH_URL https://artifacts.elastic.co/downloads/logstash/logstash-5.4.0.tar.gz

# log stash git
ENV LOGSTASH_GIT https://github.com/mypjb/logstash-docker.git

#log stash install dir
ENV LOGSTASH_PATH /usr/local/logstash

#log conf dir
ENV LOGSTASH_CONF /usr/local/logstash/conf

#COPY logstash.tar.gz ./

RUN yum update -y \
	&& yum install -y net-tools wget git java-1.8.0-openjdk


RUN wget $LOGSTASH_URL -O logstash.tar.gz \
#RUN ls \
	&& mkdir -p $LOGSTASH_PATH \
	&& tar xzf logstash.tar.gz -C $LOGSTASH_PATH --strip-components=1 \
	&& rm logstash.tar.gz \
	&& cd $LOGSTASH_PATH \
#	&& ln -s $LOGSTASH_PATH/bin/logstash /usr/local/bin \
	&& git clone $LOGSTASH_GIT logstash_git \
	&& mkdir -p $LOGSTASH_CONF \
	&& cp logstash_git/conf/* $LOGSTASH_CONF \
	&& rm -rf logstash_git


#java home
ENV JAVA_HOME /usr/lib/jvm/jre

#EXPOSE 9600

CMD $LOGSTASH_PATH/bin/logstash -f $LOGSTASH_CONF/*.conf ; /bin/bash ;

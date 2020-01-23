#logstash container image

#use official java image
FROM java:openjdk-7-jre
MAINTAINER b13n1u <b13n1u@gmail.com>


ENV LS_VERSION 1.4.2
ENV LS_PATH /logstash


RUN wget -q https://download.elasticsearch.org/logstash/logstash/logstash-$LS_VERSION.tar.gz -O - | tar zxvf - && \
    mv /logstash-$LS_VERSION $LS_PATH


#install contrib
RUN /logstash/bin/plugin install contrib

#example configuration file
ADD logstash.conf /logstash/logstash.conf


#default syslog, kibana
EXPOSE 514 9292


ENTRYPOINT ["/logstash/bin/logstash"]
CMD [ "--help"]


FROM docker.elastic.co/kibana/kibana:6.2.3
MAINTAINER libra@ljing.wang
COPY x-pack-core-6.2.3.jar /usr/share/elasticsearch/plugins/x-pack/x-pack-core/x-pack-core-6.2.3.jar

user root


RUN   yum install net-tools -y 
RUN   yum install vim -y
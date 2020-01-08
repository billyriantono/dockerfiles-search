FROM b2boost/docker-grails
MAINTAINER Luiz Muniz <luis.muniz@b2boost.com>

#

#RUN echo "deb http://packages.elastic.co/elasticsearch/2.x/debian stable main" | sudo tee -a /etc/apt/sources.list.d/elasticsearch-2.x.list
#RUN echo "deb http://packages.elastic.co/elasticsearch/1.7/debian stable main" | sudo tee -a /etc/apt/sources.list.d/elasticsearch-1.7.list
#RUN sudo apt-get update
#RUN sudo apt-get install elasticsearch

WORKDIR /root
RUN wget --quiet https://download.elastic.co/elasticsearch/elasticsearch/elasticsearch-1.7.4.zip
RUN unzip elasticsearch-1.7.4.zip
#ENV ES_MAX_MEM=1g
ENV ES_MAX_MEM=312m
#to run: elasticsearch-1.7.4/bin/elasticsearch &



WORKDIR /root
RUN wget -qO - https://www.rabbitmq.com/rabbitmq-signing-key-public.asc | sudo apt-key add -
RUN echo "deb http://www.rabbitmq.com/debian/ testing main" | sudo tee -a /etc/apt/sources.list.d/rabbitMQ.list
RUN sudo apt-get update
RUN sudo apt-get -y install rabbitmq-server
RUN rabbitmq-plugins enable rabbitmq_management


# Set Default Behavior
# Use phusion/baseimage's init system.
# See http://phusion.github.io/baseimage-docker/ for more info.
#ENTRYPOINT ["/sbin/my_init", "grails"]
#CMD ["prod", "run-war"]
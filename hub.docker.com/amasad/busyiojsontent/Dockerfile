FROM ubuntu:14.04

RUN apt-get update && apt-get dist-upgrade -y
RUN apt-get install -y zookeeper supervisor 

RUN sed -i 's/ROLLINGFILE/CONSOLE/' /etc/zookeeper/conf/environment

ADD zookeeper.conf /etc/supervisor/conf.d/

EXPOSE 2181

CMD ["supervisord", "-n"]

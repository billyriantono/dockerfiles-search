FROM       ubuntu:14.04
MAINTAINER Behance RE

RUN sudo apt-get update && apt-get install default-jre -y

ADD  https://s3-eu-west-1.amazonaws.com/softwaremill-public/elasticmq-server-0.9.3.jar /elasticmq/elasticmq-server-0.9.3.jar
ADD  run /elasticmq/run
RUN  chmod +x /elasticmq/run

EXPOSE 9324

ENTRYPOINT ["/elasticmq/run"]
CMD        []

ARG BASE_IMAGE_1=082830052325.dkr.ecr.us-east-1.amazonaws.com/devhub/builder-centos7-corretto-maven:latest
FROM $BASE_IMAGE_1
RUN yum update && yum install unzip wget
WORKDIR /tmp
RUN wget http://apachemirror.wuchna.com//ant/binaries/apache-ant-1.9.14-bin.zip
RUN unzip apache-ant-1.9.14-bin.zip
RUN rm *.zip
RUN mv apache-ant-1.9.14 ant19
RUN mv ant19 /opt

FROM alpine:latest
RUN mkdir -p /opt/ant/ant19
COPY --from=0 /opt/ant19 /opt/ant/ant19


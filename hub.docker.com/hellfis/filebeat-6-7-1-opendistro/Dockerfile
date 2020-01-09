FROM ubuntu:16.04

RUN apt-get update && apt-get install wget -y

RUN wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-oss-6.7.1-linux-x86_64.tar.gz

RUN tar -xvf ./filebeat-oss-6.7.1-linux-x86_64.tar.gz

RUN mv ./filebeat-6.7.1-linux-x86_64 /etc/filebeat

#COPY filebeat.yml /etc/filebeat/filebeat.yml

#CMD ./etc/filebeat/filebeat -e -c /etc/filebeat/filebeat.yml

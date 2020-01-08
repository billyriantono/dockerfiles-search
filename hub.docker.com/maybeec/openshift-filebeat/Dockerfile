FROM centos:7

ENV FILEBEAT_VERSION=7.3.0

# potential mounts:
# filebeat data: /var/opt/filebeat/data
# filebeat config: /etc/filebeat

RUN yum -y --setopt=tsflags=nodocs update && \
  yum -y --setopt=tsflags=nodocs install wget && \
  wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${FILEBEAT_VERSION}-x86_64.rpm && \
  yum -y install ./filebeat-${FILEBEAT_VERSION}-x86_64.rpm
  
RUN chmod -R 0777 /etc/filebeat/

WORKDIR /etc/filebeat

ENTRYPOINT [ "filebeat", "-e", "-strict.perms=false" ]

FROM medcl/centos:jdk7

#VERSION       1.0
MAINTAINER medcl,m@medcl.net,http://log.medcl.net

WORKDIR /tmp


#how to use: docker run -i -t -volumes-from jafka bin/bash
VOLUME ["/var/data/jafka"]


RUN   echo "start go." 
RUN   wget --no-check-certificate  https://googledrive.com/host/0B4VObojKr49KeVNaTnc3bDlKNXM/jafka-1.4.0-SNAPSHOT.tgz
RUN   tar -vxzf jafka-1.4.0-SNAPSHOT.tgz
RUN   mv jafka-1.4.0-SNAPSHOT /usr/local/
RUN   cp  /usr/local/jafka-1.4.0-SNAPSHOT/conf/server.properties.sample  /usr/local/jafka-1.4.0-SNAPSHOT/conf/server.properties
RUN   chmod a+x /usr/local/jafka-1.4.0-SNAPSHOT/bin/run.sh
RUN   /usr/local/jafka-1.4.0-SNAPSHOT/bin/run.sh install
RUN   rm -rif jafka-1.4.0-SNAPSHOT.tgz

CMD ["--port 9092"]

#EXPOSE 9092 

#ENTRYPOINT service jafka start
#docker run -i -t  jafka /usr/local/jafka-1.4.0-SNAPSHOT/bin/run.sh console


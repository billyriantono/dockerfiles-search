FROM ubuntu:14.04

RUN apt-get update && apt-get install -y netcat 
COPY nc2.sh /opt/
COPY tcpcontent /opt/
COPY spawner2.sh /opt/

ENTRYPOINT ["/opt/spawner2.sh"]

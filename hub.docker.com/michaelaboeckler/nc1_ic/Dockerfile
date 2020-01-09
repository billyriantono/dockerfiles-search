FROM ubuntu:14.04


RUN apt-get update && apt-get install -y netcat 
COPY nc1.sh /opt/
COPY startnc1.sh /opt/
COPY spawner1.sh /opt/
COPY tcpcontent /opt/

RUN  chmod +x /opt/nc1.sh
RUN chmod +x /opt/startnc1.sh
RUN chmod +x /opt/spawner1.sh


ENTRYPOINT ["/opt/startnc1.sh"]

FROM debian
RUN  ["/bin/bash", "-c",  "apt-get update"] 
RUN apt-get install wget -y
#ENTRYPOINT ["wget", "-O-", "-q"]
#ENTRYPOINT ["ls", "/"]
#CMD mkdir magic
CMD touch /var/alan
#CMD ls /var
#RUN apt-get install curl -y
EXPOSE 1028/tcp
LABEL maintainer="Asif Ansari"
LABEL version="2.0.1"
#ADD aa.tar /root
#COPY aa.tar  /var
VOLUME [ "/root/jack" ]


FROM java:7
MAINTAINER Nutthaphon Suwanwong

RUN (apt-get update; apt-get upgrade -y; apt-get install build-essential -y)
RUN (mv /etc/localtime /etc/localtime.old; ln -s /usr/share/zoneinfo/Asia/Bangkok /etc/localtime)
RUN (wget http://www.caucho.com/download/resin-3.1.9.tar.gz; tar -xzvf resin-3.1.9.tar.gz)

RUN (cd resin-3.1.9; ./configure; make; make install)

COPY fsis2015 /resin-3.1.9/webapps/fsis2015/

EXPOSE 8080

CMD ["java", "-jar", "/resin-3.1.9/lib/resin.jar"]

FROM chnoumis/hawtio 

RUN apt-get update && apt-get install -y ruby

ADD startup.sh /opt/tomcat/bin/startup.sh
ADD tomcat /opt/tomcat/build

CMD /opt/tomcat/bin/startup.sh

FROM gradle:jdk8-alpine

RUN mkdir -p /home/gradle/src
WORKDIR /home/gradle/src

COPY . /home/gradle/src
RUN gradle clean
RUN gradle build
RUN tar -xvf build/distributions/InterfaceConverter.tar
 
ENV JMX_PORT "9010" 

WORKDIR /home/gradle/src/InterfaceConverter/lib

EXPOSE 5001
			
CMD java  $JAVA_OPTIONS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5001 -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=$JMX_PORT -Dcom.sun.management.jmxremote.local.only=false -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -cp "*" org.z.entities.converter.Main;

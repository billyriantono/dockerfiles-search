FROM neaftw/ursi-java:1.0

COPY src/ /project/src/
COPY upload-dir/ /project/upload-dir/
COPY pom.xml /project/


RUN cd /project && mvn clean install
RUN cp /project/target/GC.war wildfly-8.2.0.Final/standalone/deployments/
ENTRYPOINT cd /project/wildfly-8.2.0.Final/bin/ && ./standalone.sh -b 0.0.0.0 -bmanagement 0.0.0.0 -DIP=$IP
#ENTRYPOINT /bin/bash

Expose 8080 5432

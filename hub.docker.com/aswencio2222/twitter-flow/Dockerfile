FROM maven:3.3.9-jdk-8
WORKDIR /source
COPY . /source
ENV MAVEN_OPTS="-Xms256m -Xmx1024m"
RUN mvn install:install-file -DgroupId=pdc -DartifactId=pln -Dpackaging=jar -Dversion=1.0-SNAPSHOT -Dfile=pln.jar -DgeneratePom=true && mvn -Pdocker clean && mvn -Pdocker package
RUN cp /source/stream/config.properties /source && cp /source/stream/log4j.properties /source && cp -r /source/stream/models /source && cp -r /source/stream/profiles /source && cp /source/stream/twitter-flow.jar /source
CMD java -jar twitter-flow.jar

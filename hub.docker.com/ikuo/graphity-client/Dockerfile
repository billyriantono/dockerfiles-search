FROM ikuo/graphity-server
MAINTAINER Ikuo Matsumura <makiczar@gmail.com>

WORKDIR /opt/
RUN wget http://repo2.maven.org/maven2/org/mortbay/jetty/jetty-runner/8.1.9.v20130131/jetty-runner-8.1.9.v20130131.jar -O /opt/jetty-runner.jar

RUN git clone https://github.com/ikuo/graphity-client.git
WORKDIR /opt/graphity-client/
RUN git checkout fix-malformedurlexception
RUN mvn package

EXPOSE 8080

CMD ["java", "-jar", "/opt/jetty-runner.jar", "target/client-1.1.1-SNAPSHOT.war"]

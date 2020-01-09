FROM ashishjain07/springdocker:latest
MAINTAINER ashish jain "ashish.jain@weightwatchers.com"
ENV MAVEN_VERSION 3.3.9

RUN mkdir -p /usr/share/maven \
  && curl -fsSL http://apache.osuosl.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
    | tar -xzC /usr/share/maven --strip-components=1 

ENV MAVEN_HOME /usr/share/maven

VOLUME /root/.m2

CMD ["mvn"]

RUN rm -rf /springdocker/
RUN git clone https://github.com/ashishse/springdocker.git /springdocker
RUN cd /springdocker &&  mvn package && java -jar target/springdocker-0.0.1.jar
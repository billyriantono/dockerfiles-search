FROM alpine
RUN apk add --update openjdk8-jre-base && rm -rf /var/cache/apk/*
ENV MVN_VER 3.3.9
ENV URI_MAVEN http://apache.ip-connect.vn.ua/maven/maven-3/$MVN_VER/binaries/apache-maven-$MVN_VER-bin.tar.gz
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk/jre
ENV PATH /opt/apache-maven-$MVN_VER/bin:$PATH
# Download and install TeamCity to /opt
WORKDIR /opt
RUN wget -O- $URI_MAVEN | tar -zx && mvn dependency:get || mvn deploy:deploy-file || echo Ok  
#RUN  mvn dependency:get -Dartifact=aumentum-registry:test:0.0.1:zip -DremoteRepositories=http://192.168.0.190:8081/content/repositories/releases/

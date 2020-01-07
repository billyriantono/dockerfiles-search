FROM eclipse/stack-base:ubuntu
EXPOSE 4403 8000 8080 9876 22

LABEL che:server:8080:ref=tomcat8 che:server:8080:protocol=http che:server:8000:ref=tomcat8-debug che:server:8000:protocol=http che:server:9876:ref=codeserver che:server:9876:protocol=http

ENV MAVEN_VERSION=3.3.9 \
    JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64 \
    VERTX_HOME=/home/user/vertx \
    TERM=xterm
ENV M2_HOME=/home/user/apache-maven-$MAVEN_VERSION
ENV PATH=$JAVA_HOME/bin:$M2_HOME/bin:$PATH
ENV VERTX_FILE=vert.x-3.1.0-full.tar.gz

RUN mkdir -p /home/user/vertx
COPY $VERTX_FILE /home/user/vertx
RUN tar -zx -f /home/user/vertx/$VERTX_FILE  --strip-components=1 -C /home/user/vertx

RUN mkdir /home/user/apache-maven-$MAVEN_VERSION && \
    wget -qO- "http://apache.ip-connect.vn.ua/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz" | tar -zx --strip-components=1 -C /home/user/apache-maven-$MAVEN_VERSION/ && \    
    echo "export MAVEN_OPTS=\$JAVA_OPTS" >> /home/user/.bashrc

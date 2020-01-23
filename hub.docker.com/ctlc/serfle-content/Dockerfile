FROM ctangqh/build-base:latest

#install openjdk
ENV JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64
ENV JRE_HOME=$JAVA_HOME/jre
ENV CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
ENV PATH=$JAVA_HOME/bin:${PATH}

RUN yum install -y java-1.8.0-openjdk-1.8.0.212.b04-0.el7_6.x86_64         \
    yum install -y java-1.8.0-openjdk-devel-1.8.0.212.b04-0.el7_6.x86_64

#install maven
ENV VERSION=3.6.1
ENV SOURCE_URL=http://apache.01link.hk/maven/maven-3/${VERSION}/binaries/apache-maven-${VERSION}-bin.tar.gz
ENV MAVEN_HOME=${AppRoot}/maven
ENV PATH=${MAVEN_HOME}/bin:$PATH

RUN mkdir -p ${MAVEN_HOME}                                                     && \                                                  
    curl -o ${RunRoot}/maven.tar.gz  ${SOURCE_URL}                             && \
    tar -zxvf ${RunRoot}/maven.tar.gz --strip-components=1 -C ${MAVEN_HOME}    && \
    rm -f ${RunRoot}/maven.tar.gz

#COPY settings.xml ${MAVEN_HOME}/conf/

RUN chown -R ${AppUser}:${AppGroup} ${MAVEN_HOME}                              && \
    chown -R ${AppUser}:${AppGroup} ${RunRoot}            

WORKDIR ${RunRoot}

CMD ["/bin/bash"]



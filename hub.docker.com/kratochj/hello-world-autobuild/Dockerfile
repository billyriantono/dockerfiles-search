FROM kratochj/tomcat:8

WORKDIR /opt

RUN curl -o apache-maven-3.3.9-bin.tar.gz http://apache.miloslavbrada.cz/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz && \
    tar xfz apache-maven-3.3.9-bin.tar.gz && \
    rm -f apache-maven-3.3.9-bin.tar.gz

ENV PATH $PATH:/opt/apache-maven-3.3.9/bin

WORKDIR /build
ADD . . 
RUN mvn clean install

RUN cp /build/target/hello-world-war*.war /build/target/ROOT.war && \
    cp target/ROOT.war /apache-tomcat/webapps
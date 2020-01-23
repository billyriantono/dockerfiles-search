FROM arkhotech/java

RUN useradd -m -d /home/java java

USER java

WORKDIR /home/java

RUN wget http://www-us.apache.org/dist/maven/maven-3/3.5.4/binaries/apache-maven-3.5.4-bin.tar.gz

RUN tar -xvf apache-maven-3.5.4-bin.tar.gz ; \
    rm apache-maven-3.5.4-bin.tar.gz 

ENV MAVEN_HOME=/home/java/apache-maven-3.5.4

ENV PATH=$MAVEN_HOME/bin:$PATH

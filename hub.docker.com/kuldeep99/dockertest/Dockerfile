FROM java:8

#ENV MAVEN_VERSION 3.2.5

#RUN curl -sSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /usr/share \
#  && mv /usr/share/apache-maven-$MAVEN_VERSION /usr/share/maven \
#  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn



#VOLUME /tmp

#ADD . /newtest

# Define working directory:
#WORKDIR /newtest

RUN ls -ltr

#RUN ["mvn", "clean", "package"]

ADD maven/springtest.jar springtest.jar

ENTRYPOINT ["java","-jar","/springtest.jar"] 
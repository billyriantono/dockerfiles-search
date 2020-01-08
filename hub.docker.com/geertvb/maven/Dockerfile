FROM geertvb/java

RUN mkdir -p /opt/maven/repository 
  
ADD http://repo1.maven.org/maven2/org/apache/maven/apache-maven/3.2.3/apache-maven-3.2.3-bin.tar.gz /opt/maven/apache-maven-3.2.3-bin.tar.gz

RUN \
  tar -xzvf /opt/maven/apache-maven-3.2.3-bin.tar.gz -C /opt/maven && \
  rm -rf /opt/maven/apache-maven-3.2.3-bin.tar.gz && \
  ln -s /opt/maven/apache-maven-3.2.3 /opt/maven/maven

ADD maven-profile.sh /etc/profile.d/maven-profile.sh

RUN chmod 755 /etc/profile.d/maven-profile.sh

VOLUME /root/.m2/repository

CMD /bin/bash -l

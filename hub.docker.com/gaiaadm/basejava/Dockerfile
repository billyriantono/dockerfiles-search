FROM java:8u45-jdk

# install Maven
ENV MAVEN_VERSION 3.3.3
RUN curl -fsSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /usr/share && \
    mv /usr/share/apache-maven-$MAVEN_VERSION /usr/share/maven && \
    ln -s /usr/share/maven/bin/mvn /usr/bin/mvn
ENV MAVEN_HOME /usr/share/maven

# install Jetty
ENV JETTY_VERSION 9.3.6.v20151106
RUN curl -fsSL http://download.eclipse.org/jetty/stable-9/dist/jetty-distribution-$JETTY_VERSION.tar.gz | tar xzf - -C /usr/share && \
    mv /usr/share/jetty-distribution-$JETTY_VERSION /usr/share/jetty && \
    ln -s /usr/share/jetty/bin/jetty.sh /usr/bin/jetty
ENV JETTY_HOME /usr/share/jetty
RUN groupadd -r jetty && useradd -r -g jetty jetty && chown jetty:jetty "$JETTY_HOME"

CMD ["/bin/bash"]

FROM ubuettgen/alpine-openjdk-jre-base 
MAINTAINER Ulrich Büttgen  "ulrich@buettgen.org"

# jetty version to use
ENV JETTY 9.2.11.v20150529

# get the tarball
RUN mkdir /opt
WORKDIR /opt
RUN echo "downloading $JETTY"
RUN wget http://download.eclipse.org/jetty/$JETTY/dist/jetty-distribution-$JETTY.tar.gz 

# extract archive
RUN tar xvzf jetty-distribution-$JETTY.tar.gz && rm jetty-distribution-$JETTY.tar.gz

# normalize folder name
RUN mv /opt/jetty-distribution-$JETTY /opt/jetty

# a simple wrapper 
ADD start.sh /opt/jetty/

#  cwd to our brand new folder
WORKDIR /opt/jetty/

EXPOSE 8080
ENTRYPOINT ["./start.sh"]

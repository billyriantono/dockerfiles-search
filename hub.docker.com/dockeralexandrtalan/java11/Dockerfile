# Oracle Java 8 Dockerfile

FROM ubuntu:16.04

ARG HOME=/usr/local/lib
ARG DEBIAN_FRONTEND=noninteractive
ARG JDK_ARCHIVE_NAME="jdk-11.0.5_linux-x64_bin.tar.gz"

WORKDIR $HOME

RUN apt-get update
RUN apt-get install -y wget

# Download and unpuck
RUN wget --no-check-certificate "https://www.dropbox.com/s/r5n0icxrils516b/jdk-11.0.5_linux-x64_bin.tar.gz?dl=0" -O $JDK_ARCHIVE_NAME
RUN tar -xvzf $JDK_ARCHIVE_NAME
RUN rm -f $JDK_ARCHIVE_NAME

#Add to PATH
ENV JAVA_HOME=$HOME/jdk-11.0.5
ENV PATH=$PATH:$JAVA_HOME/bin

RUN echo "Java has been installed:"
RUN java -version

CMD ["/bin/bash"]

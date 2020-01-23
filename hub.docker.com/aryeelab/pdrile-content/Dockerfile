# Scala, Java, and sbt for Ubuntu Latest
#
# Version     0.1

FROM dockerfile/java:oracle-java7
MAINTAINER Arun Manivannan arun@arunma.com

# install wget
RUN apt-get install -y wget

# install Scala 2.11.5
ENV SCALA_VERSION 2.11.5
ENV SCALA_DEB_FILE_NAME=scala-$SCALA_VERSION.deb

RUN wget http://www.scala-lang.org/files/archive/$SCALA_DEB_FILE_NAME
RUN dpkg -i $SCALA_DEB_FILE_NAME
RUN rm -f $SCALA_DEB_FILE_NAME

# install sbt 0.13.7
ENV SBT_VERSION 0.13.7
ENV SBT_DEB_FILE_NAME=sbt-$SBT_VERSION.deb

RUN wget https://dl.bintray.com/sbt/debian/$SBT_DEB_FILE_NAME
RUN dpkg -i $SBT_DEB_FILE_NAME
RUN rm -f $SBT_DEB_FILE_NAME

RUN sbt help

# fetches all sbt jars from Maven repo so that your sbt will be ready to be used when you launch the image
CMD ["bash"]

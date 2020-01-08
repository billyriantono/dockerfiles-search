FROM tsoftware/java8
MAINTAINER TSoftware

# install wget for downloading files
RUN apt-get install -y wget

# update apt repositories
RUN apt-get update

# scala installation
RUN wget http://www.scala-lang.org/files/archive/scala-2.11.6.deb
RUN dpkg -i scala-2.11.6.deb
RUN apt-get update
RUN apt-get install scala
RUN rm -i scala-2.11.6.deb
 
# sbt installation
RUN wget https://bintray.com/artifact/download/sbt/debian/sbt-0.13.8.deb
RUN dpkg -i sbt-0.13.8.deb
RUN apt-get update
RUN apt-get install sbt
RUN rm -i sbt-0.13.8.deb

# print versions
# fetches all sbt jars from Maven repo so that your sbt will be ready to be used when you launch the image
RUN java -version
RUN scala -version || echo '' > /dev/null
RUN sbt --version || echo '' > /dev/null
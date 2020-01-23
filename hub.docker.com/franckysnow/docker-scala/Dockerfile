FROM centos:7

RUN yum update -y
RUN yum install -y java-1.8.0-openjdk.x86_64 wget git which vim

RUN java -version
RUN echo $JAVA_HOME
RUN echo $JRE_HOME

RUN wget http://downloads.lightbend.com/scala/2.12.1/scala-2.12.1.rpm && yum install -y scala-2.12.1.rpm && rm -rf scala-2.12.1.rpm

RUN scala -version


#CMD java -version

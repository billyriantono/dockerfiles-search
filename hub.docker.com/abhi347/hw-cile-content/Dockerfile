#Source image
FROM ubuntu:14.04

#Maintainer of the file
MAINTAINER Abdul "Abdulhafis@example.com"

#updating the repository
RUN apt-get update && apt-get -y install openjdk-7-jdk wget

#Creating new path and assigning as workdir
RUN mkdir -p /usr/local/share/jboss

#creating user and assigning the same
RUN useradd jboss && groupadd test && usermod -g test jboss

#Adding the file to the work directory
#Zipping the tar file directly had issues so had to use copy command
#wget http://download.jboss.org/jbossas/7.1/jboss-as-7.1.1.Final/jboss-as-7.1.1.Final.tar.gz
#wget http://repo1.maven.org/maven2/org/jboss/modules/jboss-modules/1.1.5.GA/jboss-modules-1.1.5.GA.jar
#New jboss-module jar has to replaced cos the one present in the jboss-as-7.1.1.Final will not work
RUN wget http://download.jboss.org/jbossas/7.1/jboss-as-7.1.1.Final/jboss-as-7.1.1.Final.tar.gz
RUN gunzip *.gz
RUN tar -xvf jboss-as-7.1.1.Final.tar
RUN cp -pr jboss-as-7.1.1.Final /usr/local/share/jboss/jboss-as-7.1.1.Final
RUN rm jboss-as-7.1.1.Final.tar
RUN wget http://repo1.maven.org/maven2/org/jboss/modules/jboss-modules/1.1.5.GA/jboss-modules-1.1.5.GA.jar
RUN cp -p jboss-modules-1.1.5.GA.jar /usr/local/share/jboss/jboss-as-7.1.1.Final/jboss-modules.jar

#Setting the user permission
RUN chown -R jboss:test /usr/local/share/jboss/*

#Defining Jboss home env
ENV JBOSS_HOME /usr/local/share/jboss/jboss-as-7.1.1.Final/

# create JBoss console user
RUN $JBOSS_HOME/bin/add-user.sh admin admin@2016 --silent=true

# configure JBoss
RUN echo "JAVA_OPTS=\"\$JAVA_OPTS -Djboss.bind.address=0.0.0.0 -Djboss.bind.address.management=0.0.0.0\"" >> $JBOSS_HOME/bin/standalone.conf

# JBoss ports
EXPOSE 8080 9990 9999

#Starting jboss
CMD ["/usr/local/share/jboss/jboss-as-7.1.1.Final/bin/standalone.sh" , "-b" , "0.0.0.0" ]

USER jboss

FROM java:8

MAINTAINER Vincent RAVERA <ravera.vincent@gmail.com>

WORKDIR /home/root/Application
#COPY src /home/root/Application/src
#RUN mkdir bin
#RUN javac -d bin src/HelloWorld.java
RUN apt-get update
RUN apt-get install -y wget
RUN wget http://apache.crihan.fr/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
RUN tar -xvzf apache-maven-3.3.9-bin.tar.gz
RUN rm apache-maven-3.3.9-bin.tar.gz
RUN ln -s /home/root/Application/apache-maven-3.3.9/bin/mvn /bin
#ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]

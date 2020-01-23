FROM java:8
MAINTAINER Docker Training <boris.slavin@mheducation.com>
COPY src /home/root/javahelloworld_github.com/src
ENV FOO bar
ENV JAVA_HOME /usr/bin/java
WORKDIR /home/root/javahelloworld_github.com
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN wget cnn.com
#ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]

# ex8.8
RUN mkdir /data/myvol -p
RUN echo "put some text here" > /data/myvol/test
VOLUME /data/myvol

FROM java:7
ENV FOO bar
COPY src /home/root/javahelloworld/src
#RUN javac HelloWorld.java 
WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN apt-get update
RUN apt-get install -y emacs 
ENTRYPOINT ["java","-cp","bin","HelloWorld"]

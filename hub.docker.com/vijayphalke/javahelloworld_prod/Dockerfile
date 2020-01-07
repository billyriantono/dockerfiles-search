FROM java:7
ENV FOO bar
WORKDIR /home/root/javahelloworld
COPY src /home/root/javahelloworld/src
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN apt-get install -y git 
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
#docker run -it --entrypoint bash docker/myjavaimage


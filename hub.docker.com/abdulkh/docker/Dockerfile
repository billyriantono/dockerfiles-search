FROM java:7-jdk
COPY /src/ /test/
RUN cd /test && javac com/abdul/docker/sample/HelloWorld.java
WORKDIR /test
CMD ["java","com.abdul.docker.sample.HelloWorld"]
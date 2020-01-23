FROM java:7
RUN apt-get update
RUN apt-get install -y wget curl
ADD src /root/javahelloworld/src/
WORKDIR /root/javahelloworld/
RUN mkdir bin
RUN echo "Hello world build..."
RUN ["javac","-d","bin","src/HelloWorld.java"]
RUN echo "Test 2"
ENTRYPOINT ["java","-cp","bin","HelloWorld"]

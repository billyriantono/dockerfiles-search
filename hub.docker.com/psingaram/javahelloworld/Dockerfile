FROM java:8
MAINTAINER Docker Training <education@docker.com>
COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld
ADD /src /myapp/src
RUN mkdir bin
RUN mkdir prab
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]

FROM java:7
COPY  bin /home/root/javahelloworld/bin
WORKDIR /home/root/javahelloworld
RUN javac -d bin bin/HelloWorld.java
RUN mkdir toto
ENTRYPOINT ["java","-cp","bin","HelloWorld"]
ENV FOO bar 

FROM java:7
COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld
ENV FOO bar
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
CMD ["java", "-cp", "./bin", "HelloWorld","Hello Al"]
ENTRYPOINT ["java","-cp","./bin","HelloWorld"]

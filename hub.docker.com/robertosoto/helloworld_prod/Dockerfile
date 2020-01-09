FROM openjdk:8
WORKDIR /home/root
RUN mkdir javahelloworld
RUN mkdir javahelloworld/bin
RUN mkdir javahelloworld/src
COPY src/HelloWorld.java javahelloworld/src
RUN javac -d javahelloworld/bin javahelloworld/src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "javahelloworld/bin", "HelloWorld"]


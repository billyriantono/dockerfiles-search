FROM java:8

#COPY HelloWorld.java /
#RUN javac HelloWorld.java
#ENTRYPOINT ["java","HelloWorld"]

COPY src /home/root/javahelloworld/src 
RUN touch tata
WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java","-cp","bin","HelloWorld"]

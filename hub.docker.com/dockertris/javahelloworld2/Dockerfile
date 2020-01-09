FROM java:7
ENV FOO bar
WORKDIR /home/root/javahelloworld
COPY src src
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
RUN mkdir /data/myvol -p
RUN echo "toto tata" > /data/myvol/test
VOLUME /data/myvol
#ENTRYPOINT ["java","-cp","bin","HelloWorld"]




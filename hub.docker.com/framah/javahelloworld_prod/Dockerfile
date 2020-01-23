FROM java:7

ENV FOO bar

WORKDIR /home/root/javahellow

RUN mkdir bin

COPY src /home/root/javahellow/src
RUN javac -d bin src/HelloW.java

ENTRYPOINT ["java","-cp","bin","HelloW"]

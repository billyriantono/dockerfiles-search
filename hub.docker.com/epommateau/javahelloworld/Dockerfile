FROM java:8

COPY src /root/src

WORKDIR /root/

RUN mkdir bin && javac -d bin src/HelloWorld.java


ENTRYPOINT ["java","-cp","bin","HelloWorld"]

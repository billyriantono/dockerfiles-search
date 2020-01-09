FROM java:7

WORKDIR /home/root/javahelloworld
RUN mkdir -p /home/root/javahelloworld
COPY src src
RUN set -x && \
    mkdir -p bin && \
    javac -d bin src/HelloWorld.java

ENV ZENIKA=Rulez \
    LILLE=null

RUN apt-get install -y curl

ENTRYPOINT ["java","-cp","bin","HelloWorld"]



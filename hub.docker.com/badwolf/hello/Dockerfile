FROM arthurcarlsson/jdk9
MAINTAINER  <badwolf09950@gmail.com>

RUN mkdir /hello

ADD ./Hello.java /hello

WORKDIR /hello

RUN javac Hello.java

ENTRYPOINT ["java" ,"Hello"]
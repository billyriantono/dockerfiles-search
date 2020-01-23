# Run this using:
# $ docker run -d -p 5000:5000 -v `pwd`:/encelladus onekey-api
# or simply:
# $ ./gradlew run

FROM ubuntu:latest

MAINTAINER Arturo Blas Jimenez "a.blas@actisec.com"

ADD ./configDependencies.sh /configDependencies.sh

RUN chmod 755 /configDependencies.sh

RUN ./configDependencies.sh

WORKDIR /encelladus

ENV PORT 5000

EXPOSE 5000 

ENTRYPOINT ["./run.sh", "foreground"]


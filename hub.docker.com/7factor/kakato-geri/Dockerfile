FROM openjdk:11-jdk

RUN mkdir -p /karate
RUN wget https://dl.bintray.com/ptrthomas/karate/karate-0.9.2.jar -O /karate/karate.jar
COPY scripts/karate /usr/bin/karate
RUN chmod 755 /usr/bin/karate

ENTRYPOINT ["karate"]
FROM openjdk:8-jdk

ENV VERSION 2.2.3

RUN curl -sSLo /apache-archiva-$VERSION-bin.tar.gz https://archive.apache.org/dist/archiva/$VERSION/binaries/apache-archiva-$VERSION-bin.tar.gz \
  && tar --extract --ungzip --file apache-archiva-$VERSION-bin.tar.gz --directory / \
  && rm /apache-archiva-$VERSION-bin.tar.gz && mv /apache-archiva-$VERSION /apache-archiva


ENV ARCHIVA_BASE /apache-archiva
WORKDIR /apache-archiva

VOLUME /apache-archiva/data
VOLUME /apache-archiva/logs
VOLUME /apache-archiva/repositories
VOLUME /apache-archiva/temp
VOLUME /apache-archiva/conf

EXPOSE 8080
CMD bin/archiva console
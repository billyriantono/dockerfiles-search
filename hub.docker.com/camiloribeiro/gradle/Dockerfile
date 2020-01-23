FROM java:8

WORKDIR /gradle
RUN apt-get update && apt-get -y install zip unzip
RUN curl -s https://downloads.gradle.org/distributions/gradle-1.10-bin.zip > gradle.zip
RUN unzip gradle.zip -d /lib && rm -f gradle.zip

ENTRYPOINT ["/lib/gradle-1.10/bin/gradle"]
CMD ["tasks"]

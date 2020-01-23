FROM openjdk:10-jre-slim
ENV NEM2CAMEL_TAG=v0.1.1
WORKDIR /tmp
RUN apt-get update -y && apt-get upgrade -y \
  && apt-get install -y --no-install-recommends git gnupg \
  && echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list \
  && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823 \
  && apt-get update -y \
  && apt-get install -y --no-install-recommends sbt
RUN git clone --depth=1 -b $NEM2CAMEL_TAG https://github.com/nemtech/nem2-camel.git \
  && cd nem2-camel \
  && sbt assembly \
  && mkdir -p /opt/nemtech/bin/ \
  && cp target/scala-2.12/nem2-camel.jar /opt/nemtech/bin/
FROM openjdk:10-jre-slim
EXPOSE 9000
WORKDIR /opt/nemtech/bin/
COPY --from=0 /tmp/nem2-camel/target/scala-2.12/nem2-camel.jar ./
ENTRYPOINT ["java", "-jar", "nem2-camel.jar"]
CMD ["--help"]

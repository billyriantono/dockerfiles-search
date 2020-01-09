FROM frolvlad/alpine-oraclejre8:slim
MAINTAINER ybd <yangbingdong1994@gmail.com>
ADD elastic-job-lite-console.tar.gz /
WORKDIR elastic-job-lite-console
ENTRYPOINT exec java -classpath ./lib/*:. io.elasticjob.lite.console.ConsoleBootstrap 8080

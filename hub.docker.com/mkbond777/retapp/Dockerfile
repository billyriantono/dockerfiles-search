FROM ysihaoy/scala-play:2.12.2-2.6.0-sbt-0.13.15
#FROM ubuntu
MAINTAINER mkbond777@hotmail.com

# caching dependencies
#COPY ["build.sbt", "/tmp/build/"]
#COPY ["project/plugins.sbt", "project/build.properties", "/tmp/build/project/"]
#RUN cd /tmp/build && \
# sbt compile && \
# rm -rf /tmp/build

# copy code
COPY . /root/app/
WORKDIR /root/app
RUN sbt dist
#RUN ls target/universal
#COPY ["target/universal/retapp-1.0.0-SNAPSHOT.zip", "/"]
#WORKDIR /
WORKDIR target/universal
RUN unzip retapp-1.0.0-SNAPSHOT.zip
EXPOSE 9000
CMD ["retapp-1.0.0-SNAPSHOT/bin/retapp"]

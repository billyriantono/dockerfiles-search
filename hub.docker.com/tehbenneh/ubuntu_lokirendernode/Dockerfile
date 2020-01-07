FROM debian:latest
MAINTAINER Ben Harker (benharker@mac.com)

RUN apt-get update && apt-get install wget blender default-jre -y ;
RUN wget http://kent.dl.sourceforge.net/project/loki-render/loki-render/0.7.2/LokiRender-072.jar -O /LokiRender-072.jar ;

CMD ["java", "-jar", "/LokiRender-072.jar", "/usr/bin/blender", "10.2.0.27"]

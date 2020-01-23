#
# Build image : 
# docker build .
#
# 
# Create service:
# docker-compose up --not-start
#
# Start:
# docker-compose start
#
#
# Connect bash
# docker exec -it name of the image sh
#
#

FROM openjdk:8-jre-alpine
VOLUME /tmp
ADD target/'name of your app'.jar app.jar
ENV JAVA_OPTS=""

ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -jar /app.jar" ]
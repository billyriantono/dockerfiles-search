FROM openjdk:8-jre-slim

# building from openjdk debian
RUN apt update
RUN apt install python3-pip curl -y
RUN pip3 install requests numpy==1.16.5 geopy
RUN pip3 install obspy

COPY post-bulletins-3.10.27 /opt/post_bulletins
COPY mag /mag
WORKDIR /opt/post_bulletins
ENTRYPOINT ["java", "-jar", "jruby-complete.jar", "post_bulletins.rb"]